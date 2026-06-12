---
template: post
title: "Multi-cloud infra that is cheap, boring and low maintenance"
date_published: 1781248151511
amp: true
---

As a solo developer, or indie hacker, staff loop engineer, I deploy and manage a multitude of applications.

Most of these services are deployed in [Railway](https://railway.com). But as you know, Railway hasn’t had the perfect track record[^1] for being [up and reliable](https://status.railway.com/historical). Hence I decided to venture into a multi-cloud deployment strategy so that I don’t have to wake up at midnight (thanks PagerDuty) and apologise to my users.

Unfortunately, when Railway is down, there isn’t much I can do other than wait for them to come back, the only real solution was going multi-cloud.

## What do we need?

I needed a platform other than Railway that could pretty much mirror my entire deployment, except it should be serverless (containers that can scale to zero), so that it only runs as a backup when needed and doesn’t charge me for the entire time it’s deployed. It also had to support fast switchover with minimal disruption to the service.

The second thing I wanted to fix was my database. I co-located all my applications and the database together in Railway, but the database being down caused a lot more problems than I anticipated (duh!). So I decided to move that to the best database platform ever, [PlanetScale](https://planetscale.com/metal) <3.

Finally, I needed a load balancer that could detect when my main deployment in Railway is down and gracefully fall back to the backup.

## How do we do it?

After digging around a bit, I decided to go with [Google Cloud Run](https://cloud.google.com/run). I had already played around with it before. It worked great, it was very straightforward, and it scaled exactly the way I wanted it to, unlike AWS App Runner, which for some reason just wouldn’t scale up fast enough (skill issue?).

For the load balancer, I was familiar with [Cloudflare](https://developers.cloudflare.com/load-balancing), so without much research I just went for it. There is a main pool, which has all the Railway services, and then there is the fallback pool, GCP. Cloudflare continuously does health checks against the main pool, and every time the main pool is down, it will route requests to the fallback pool. Don't forget to enable [Adaptive routing](https://developers.cloudflare.com/load-balancing/understand-basics/adaptive-routing/).

BTW, the main pool itself has a small load balancing setup inside it, where 90% of the traffic goes to the main production servers, but 10% goes to the pre-prod servers, which I use for [canary rollout](https://launchdarkly.com/blog/four-common-deployment-strategies/).

To summarise, there is a Cloudflare load balancer at the edge, user request hits that first, it is then routed to Railway or GCP, depending on the health of the services. The database layer is completely moved to PlanetScale Metal instances.

I think it’s simple, cheap and low maintenance, exactly how infrastructure should be.

## There are ~~caveats~~ tradeoffs

- DB is still a single point of failure, but I trust PlanetScale
- Requests could be slower while the failover happens, Cloud run might take a while to warm up, but its always better to have a slower response than "no" response. [^2]
- Any infra changes needs to be applied in two places, Railway and GCP

[^1]: Incidents happened few weeks before the time of writing, in no way am I saying they will be like this forever. Railway is awesome and they're working on it.

[^2]: You can work around this by settings minimum instance count, but then you're always paying for those instances.
