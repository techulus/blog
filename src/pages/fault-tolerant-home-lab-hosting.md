---
template: post
title: "Fault tolerant home lab hosting"
date_published: 1663806443000
cover: /cover/buttons.jpeg
amp: true
---

I've been self-hosting stateless web services at my home lab for over two years now, so it's time to write about it. To be clear, I'm not implying this is the right method, it is what has worked best for me.

> The concept is straightforward, all user requests will first hit a CDN / Load balancer, it will then forward that request to your home lab if it is alive, or else it will forward the request to a backup cloud serverless instance.

Prerequisites:

* Your web service is **stateless**, [read more](https://www.proud2becloud.com/stateful-vs-stateless-the-good-the-bad-and-the-ugly/?ref=techulus.xyz).
    
* Your web service can be accessed publically, so that CDN / load balancer can access it.
    

### Step 1: Replicate your web service in the cloud

You can set this up by using [AWS App runner](https://aws.amazon.com/apprunner/?ref=techulus.xyz) or [Google Cloud run](https://cloud.google.com/run?ref=techulus.xyz), it won't cost much as this instance will be used as a backup and will only process requests if your home lab is unable to accept requests.

### Step 2: Setup a CDN / Load balancer

I'm using AWS Cloudfront as it's cheap and can handle our failover logic, you could achieve the same setup using a Cloudflare load balancer, but it could cost more depending on your usage. Here is a neat diagram to explain the setup:

![Fault tolerant home lab hosting](/images/homelab-hosting/cloudfront.png)

So go ahead and create a Cloudfront distribution for your web service, add your home lab web service URL as the origin and deploy it. Make sure it's up and update the DNS configuration (if required) so that your domain name points to CDN, once this is done, all your requests should be served via CDN.

Next, we will create another origin for our cloud instance, and then create an origin group to handle the failover, it will look like this:

![Fault tolerant home lab hosting](/images/homelab-hosting/origins.png)

The final step is to update our distribution behaviour, we will update the default rule to use our origin group instead of the home lab one and it is done!

So every time a request hits the CDN, it will first try processing the request using the home lab instance, if for some reason the request fails, it will be retried using the cloud instance of the same service and all this happens seamlessly with minimal impact on user experience.

If you were to use Cloudflare Load Balancer, we would achieve the same setup by using multiple origins and health checks.