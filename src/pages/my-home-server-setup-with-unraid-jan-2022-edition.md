---
template: post
title: "My home lab setup with UNRAID, Jan 2022 edition"
date_published: 1642548443000
cover: https://images.unsplash.com/photo-1558494949-ef010cbdcc31?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxMTc3M3wwfDF8c2VhcmNofDF8fHNlcnZlcnxlbnwwfHx8fDE2NDI1NzIyNDU&ixlib=rb-1.2.1&q=80&w=2000
---

I'm going to walk you through my home lab setup, showing you what I've set up now, both hardware and software and also share my plans for potential upgrades in the future.

> This post contains affiliate links. If you use these links to buy something we may earn a commission. Thanks.

## Hardware

We will begin with the hardware, I have a basic home lab setup with just two servers, one is a used Dell Optiplex 7050 Micro used as a web server, the other is a custom build tower PC that acts as my gaming PC, NAS and is also hosting several services. They're connected using a [TP-Link AX6000 Wifi 6 router](https://www.amazon.com/gp/product/B07L56SN8M/ref=as_li_qf_asin_il_tl?ie=UTF8&tag=dotvim-20&creative=9325&linkCode=as2&creativeASIN=B07L56SN8M&linkId=8cc2619585422add854b25143473a4fa&ref=techulus.xyz) with a gigabit internet connection.

*Specifications for Dell Optiplex 7050* ***aka Hades***  
Core™ i5-6600, 16GB RAM, 256GB SSD

![My home lab setup with UNRAID, Jan 2022 edition](https://cdn.hashnode.com/res/hashnode/image/upload/v1682040962583/eee77ebc-c421-4c93-8d0f-4c90ee597d46.png)

*Specifications for Tower PC* ***aka Thor***  
Core™ [i5-11600K](https://www.amazon.com/gp/product/B08X67YZBL/ref=as_li_qf_asin_il_tl?ie=UTF8&tag=dotvim-20&creative=9325&linkCode=as2&creativeASIN=B08X67YZBL&linkId=1a7a54da13a770d7c2a18c3808055718&ref=techulus.xyz), ROG STRIX B560-G Motherboard, [32GB RAM](https://amzn.to/3qEI816?ref=techulus.xyz), 4TB storage (2x 1TB NVMe drive, 1x 2TB HDD), [Nvidia RTX 3060](https://www.amazon.com/gp/product/B0971B5B1L/ref=as_li_qf_asin_il_tl?ie=UTF8&tag=dotvim-20&creative=9325&linkCode=as2&creativeASIN=B0971B5B1L&linkId=ffb81beb4594222b539bb0578eeb6317&ref=techulus.xyz) and the most important part RGB (for extra FPS)

![My home lab setup with UNRAID, Jan 2022 edition](https://cdn.hashnode.com/res/hashnode/image/upload/v1682040964626/f741db37-f735-458f-b90f-b46b95f77192.jpeg)

## Software

Starting with Dell, it has a super simple setup with just Ubuntu and docker. Essentially, it is a docker swarm worker node that connects to a swarm leader hosted in [DigitalOcean](https://www.digitalocean.com/?refcode=aed42342d15d&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge) and its only purpose is to run production workloads assigned by the leader. It also runs my homebridge docker container, I'm too lazy to move it to my UNRAID server. You might be wondering why docker swarm? why not Kubernetes or Nomad? I chose docker swarm because it takes barely 2 mins to set everything up and I didn't want to go through the elaborate set-up process which is required for most container orchestration managers.

Coming to the tower PC, it runs on [UNRAID](https://unraid.net/?ref=techulus.xyz) OS, which is unbelievably easy to set-up and has an amazing community. I don't want to go too deep into UNRAID now, maybe another time, but for now here are the things I've running on it:

![My home lab setup with UNRAID, Jan 2022 edition](https://cdn.hashnode.com/res/hashnode/image/upload/v1682040966621/d9c1dd5d-1078-4f60-8e1f-017b3e49d1a5.png)

UNRAID Array

* my NAS
    
* time machine backup drive which is technically part of the NAS
    
* a Windows VM with GPU passthrough as my gaming PC
    
* an Ubuntu server VM, second docker swarm worker node that joins the cloud leader and runs some production workloads
    
* a HiveOS VM for crypto mining
    
* another Ubuntu server VM for running this blog
    

![My home lab setup with UNRAID, Jan 2022 edition](https://cdn.hashnode.com/res/hashnode/image/upload/v1682040968470/d1b35523-5cdc-49bc-ba49-9118ba82acf6.png)

VMs and Docker containers

And lots of docker containers:

* [Tailscale](https://tailscale.com/?ref=techulus.xyz) for my private VPN
    
* [Netdata](https://www.netdata.cloud/?ref=techulus.xyz) for monitoring
    
* [Uptime Kuma](https://github.com/louislam/uptime-kuma?ref=techulus.xyz) for status checks
    
* [Speed test tracker](https://github.com/henrywhitaker3/Speedtest-Tracker?ref=techulus.xyz) which periodically runs speed tests
    
* [Plex](https://www.plex.tv/?ref=techulus.xyz) Media Server
    
* [Nginx Proxy Manager](https://nginxproxymanager.com/?ref=techulus.xyz)
    
* [Commento](https://commento.io/?ref=techulus.xyz) for my blog comments
    
* Postgres DB and Adminer
    
* Private Docker registry
    

## What's next?

These are my highly optimistic plans, kind of like my dream setup.

* Add more mini/micro servers for horizontally scaling my web services, this would depend on the load also, so only if required.
    
* Upgrade to Ryzen™ 9 [5900X](https://www.amazon.com/gp/product/B08164VTWH/ref=as_li_qf_asin_il_tl?ie=UTF8&tag=dotvim-20&creative=9325&linkCode=as2&creativeASIN=B08164VTWH&linkId=5674bf08947f829512faaf95d99ff5d5&ref=techulus.xyz)/[5950X](https://www.amazon.com/gp/product/B0815Y8J9N/ref=as_li_qf_asin_il_tl?ie=UTF8&tag=dotvim-20&creative=9325&linkCode=as2&creativeASIN=B0815Y8J9N&linkId=1ee30dd750134fa546cbd4ec7792b90b&ref=techulus.xyz) (definitely not cheap) for the extra cores (12/16), this would require a new motherboard also.
    
* Add more storage, get it up to 8 or 12TB.
    
* Replace TP-Link router with [UniFi Dream Machine Pro](https://www.amazon.com/gp/product/B086967C9X/ref=as_li_qf_asin_il_tl?ie=UTF8&tag=dotvim-20&creative=9325&linkCode=as2&creativeASIN=B086967C9X&linkId=fb978c3c596b7aaf091b430d677e492b&ref=techulus.xyz), PoE injector and WiFi access points.
    
* Setup an offsite backup, explore cloud options.
    

### 🚨 Mar 2022 Update

* I've added another Dell OptiPlex machine (aka Athena) with nearly identical specs.
    
* I got rid of Docker swarm as it had reliability issues, unfortunately, I couldn't identify the exact problem and I didn't want to spend too much time debugging. The new setup is even more basic, I simply run multiple instances of Docker containers and load balance using NGINX. This new setup without any sort of container orchestration might seem like it's less reliable, but I've other measures in place to prevent downtime, I'll write about it soon.
    
* Replaced commento with [https://utteranc.es](https://utteranc.es/?ref=techulus.xyz) because I like the look and feel of GitHub comments, also it's less work to maintain.
    
* I've added a VM for running [https://temporal.io](https://temporal.io/?ref=techulus.xyz), it doesn't do anything at the moment, I'm just playing around and learning to run workflows using Temporal.