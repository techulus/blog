---
template: post
title: "The Web Badging API"
date_published: 1572823643000
cover: /images/badge/cover.png
---

We web developers always strive to make our “web apps” perform and feel as native as possible, but our capabilities are always limited by what is provided by browsers. Thankfully, the web ecosystem is evolving at a quick pace and we’re frequently introduced to new powerful APIs that lets us build more advanced tools. Let’s have a look at such a new API that bridges the gap between web and native applications.

Web Badging API is a proposed platform API that allows web apps to set badges associated with an open page (such as when a badge is shown on or near the page’s icon in a browser tab) and app-wide badge in operating-system-specific places such as the shelf or home screen. Basically, it lets your app show badges like this:

![The Web Badging API](/images/badge/1.png)

PWA with Badge on macOs

and like this:

![The Web Badging API](/images/badge/2.png)

Windows taskbar badge

![The Web Badging API](/images/badge/3.png)

Badge on Android

Some use cases for this API include; showing the number of unread items or messages, a subtle nudge to notify users that something is waiting inside the app, etc.

It has been available as [*origin trial*](https://googlechrome.github.io/OriginTrials/?ref=techulus.xyz) on Chrome since version 73 (Windows 7+ and macOS) and lets you use the Badging API when the user has an installed app.

As per WICG docs using the API is simple, you can set a badge using: `navigator.setClientBadge(5);` // sets numeric badge with value 5

and clear the badge using: `navigator.clearClientBadge();`

Since this is an experimental API in Chrome the implementation differs from the WICG proposal. You should use `ExperimentalBadge.set` instead of `navigator.setClientBadge`

`window.ExperimentalBadge.set(5);` // to set

View [Badging API Demo](https://badging-api.glitch.me/?ref=techulus.xyz) in Chrome, you can also find its [source code here](https://glitch.com/edit/?ref=techulus.xyz#!/badging-api?path=demo.js).

To know more checkout [WICG explainer](https://github.com/WICG/badging/blob/master/explainer.md?ref=techulus.xyz) and Chrome [Badging API](https://web.dev/badging-api/?ref=techulus.xyz).  
You can read more about the host implementation [here](https://github.com/WICG/badging/blob/master/docs/implementation.md?ref=techulus.xyz).
