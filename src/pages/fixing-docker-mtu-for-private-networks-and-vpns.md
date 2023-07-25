---
template: post
title: "Fixing Docker MTU for private networks and VPNs"
date_published: Tue Jan 25 2022
cover: https://images.unsplash.com/photo-1613690399151-65ea69478674?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxMTc3M3wwfDF8c2VhcmNofDV8fGNvbnRhaW5lcnxlbnwwfHx8fDE2NDMwNzcxOTA&ixlib=rb-1.2.1&q=80&w=2000
---

Recently while settings up a Docker swarm cluster I noticed something strange happening, a lot of the requests being processed by the swarm service were failing even though the cluster was live and the nodes were able to communicate to each other. After a few hours of debugging, scratching heads, googling etc I finally found [this](https://github.com/moby/moby/issues/36689?ref=techulus.xyz) and that was indeed the problem.

In a nutshell, the problem was the swarm ingress routing mesh with a bad MTU configuration, so even though the nodes could communicate to each other, some of the TCP packets could not be sent over the network because of its size.

💡 The internet's transmission control protocol (TCP) uses the MTU to determine the maximum size of each packet in any transmission. MTU is usually associated with the Ethernet protocol, where a **1500-byte packet is the largest allowed in it** (and hence over most of the internet).

The Docker Daemon does not check the MTU of the outgoing connection and is by default set to 1500, my private network (using [Tailscale](https://tailscale.com/?ref=techulus.xyz)) on the hand only supports an MTU of 1280, you can find this by running `ip link` command.

![Fixing Docker MTU for private networks and VPNs](https://cdn.hashnode.com/res/hashnode/image/upload/v1682040948447/8ed65b94-a568-4c86-b739-84445b548575.png)

The solution is fairly straightforward, we have to update Docker network configuration to use the lower MTU and we can do this in two ways:

### Create new ingress

* Stop all services and delete the current ingress using `docker network rm ingress`
    
* Create new ingress network with updated MTU, `docker network create --driver overlay --ingress --opt com.docker.network.driver.mtu=1280 --subnet 10.11.0.0/24 --gateway 10.11.0.1 ingress`
    
* Restart docker and deploy your services again.
    

### Configure using docker compose

Another solution is to provide this configuration in your `docker-compose` file.

```yaml
networks:
    default:
        driver: bridge
        driver_opts:
            com.docker.network.driver.mtu: 1280
```

*References:*  
https://mlohr.com/docker-mtu/