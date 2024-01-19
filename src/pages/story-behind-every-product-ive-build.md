---
template: post
title: "Story behind every product I've build - Part 1 of ?"
date_published: 1670110043000
cover: /cover/story.jpeg
---

It was 2009, I got my hands on an iPhone (the original iPhone 2G) for the very first time. It was uncommon in India, mainly because it was hard to get and not affordable, but more than that it wasn't a great experience. All the phones were locked and also jailbroken for unlocking, we couldn't update iOS because that would break Cydia and get rid of the carrier unlock. Unaware of this the first thing I did after getting the phone was to upgrade the OS and thus got my phone locked, sigh.

I remember spending the whole night with my father trying to fix it, a lot of googling, reading and comprehending what had happened, and I found a solution. I was lucky and the version I had upgraded to had a jailbreak, phew. I downloaded the windows app and followed the steps and voila I had officially jailbroken my iPhone. I installed the unlock using Cydia, (it was called ultrasn0w) and successfully unlocked the iPhone.

After this journey, I decided to create a blog, to share tutorials, and guides on everything related to iPhone, iOS, and Jailbreaking, thus born the Techulus iBlog. It was the first thing I created, but sadly it didn't last very long.

> Fun fact, I lost techulus.com domain name for a while. How? I forgot to renew it.

A few years pass, and my interests eventually moved away from all that to software engineering, I enjoyed coding more than anything. I am in Uni now, studying computer science and I started with simple HTML-CSS projects and eventually graduated to PHP. To be honest, I didn't know much about real-world applications even though I was nearly done with my computer science degree, I could build some basic PHP apps. At the time myself and my classmate/best bud decided to build FindMyBoat, it was a marketplace for finding houseboats (was a huge deal back then). It was a shitty version of booking.com without the actual booking system. The project didn't go anywhere but we learned a valuable lesson, dealing with people is hard. In 2015 I made the project open source, heads up, the code is terrible.

[https://github.com/arjunkomath/findmyboat](https://github.com/arjunkomath/findmyboat)

After Uni, I had some free time, so I build a flappy bird clone for Android, there is no real story behind this, was bored and hungry for knowledge.

[https://github.com/arjunkomath/Trap-Down-Android-Game](https://github.com/arjunkomath/Trap-Down-Android-Game)

Moving on, I got my first job, I was consuming knowledge at an extremely fast pace, I'm exploring tons of things and that is how I landed in the Javascript world. React & Nodejs is the hype and I'm in love with it. I always build some sort of application to learn things, and it was at this time I build Wush.XYZ (Wush stand for web push).

Wush was sort of a mix of intercom chat and targeted web push notifications. Wush had an interesting stack, it was built using Sails JS ([https://sailsjs.com](https://sailsjs.com/?ref=techulus.xyz)) as the framework came with socket.io out of the box, there was no frontend framework, and all pages were server-side rendered, MongoDB for the database and deployed to AWS using EC2. Sadly it didn't last long, I had very few paying customers and hence the project was killed.

Fast forwarding through some random stuff:

* An app for creating a list of products with affiliate links (basically a clone of [https://kit.co](https://kit.co/?ref=techulus.xyz), which I didn't know).
    
* A public API for storing JSON, it was called JaaS aka JSON-as-a-service, it was inspired by a product I saw in product hunt called boolean as a service.
    
* And several small open-source projects.
    

My first mobile app was an Android app called Honest review. An app that let users review the device that was running the app, hence 100% legit honest reviews. You could only use the app after reviewing your device, it was part of the sign-up process. Once you got in, you could read other reviews and discuss with other members about other devices. The same story as before, no real user base and it was killed. It was live on the play store for a very long time though.

> After building so many things I couldn't bother buying domain names for every one of them, so I just started using subdomains. This is a bad idea.

After entering the mobile development arena, I was pretty frustrated with Java & Objective-C, it was too much effort and a massive learning curve to build anything good on Android or iOS. Hybrid apps were terrible and I didn't want anything to do with it. But then there was React Native, and it was awesome. Following my usual strategy, I decided to build an app to learn React Native and thus Feline for product hunt came to life. It's an open-source mobile client for product-hunt and was available for free on Play Store. In case you're wondering why I didn't publish anything on the App Store, it's because I couldn't justify spending $99 every year for publishing a free app.

It's been more than 5 years or 6 years since I've started building random things on the internet. One fine day I'm working on building a pre-rendering solution for an Angular app and I come across puppeteer. It was a library for programmatically controlling the chrome browser and it could do a lot of things, the one particular feature that caught my attention was capturing screenshots. I was like, *nice, that is cool, I could build an API for this!* I Google about this and there are a bunch of big players in this space, URL2PNG, URLBOX etc, but all of them are subscription-based and are pretty expensive. So I decided to build something similar, but instead of a subscription, it will be usage-based and will be much cheaper than the competition, and that is [Capture by Techulus](https://github.com/arjunkomath/Feline-for-Product-Hunt).

Capture has been live for more than 6 years now and it doing amazing, it has captured over 12.4 million unique pages. I've rewritten the entire app and APIs from scratch twice, and I've hosted it in Azure, AWS, DigitalOcean and now on Google cloud. It has been an amazing journey and I'm sure the future will be even more exciting.

Let's end part one here, I learned a lot from building and running Capture and it has influenced the way I build things from then on, I'll share more in Part two.