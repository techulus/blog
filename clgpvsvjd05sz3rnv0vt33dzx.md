---
title: "My First VS Code Extension"
datePublished: Thu May 10 2018 16:55:46 GMT+0000 (Coordinated Universal Time)
cuid: clgpvsvjd05sz3rnv0vt33dzx
slug: my-first-vs-code-extension
canonical: https://techulus.xyz/my-first-vs-code-extension/
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682041031187/aefb63d3-40ba-4ca8-8adb-0a69a1477f03.png

---

> Finally, after playing around with VS Code a lot, I decided I should publish a plugin. I had a few ideas in mind, mostly minor helpers that would help me in my work.

I started off with a simple yet useful extension. I work with Javascript code every day, it could be React or NodeJS, mostly microservices build on AWS Lambda. I used to manually add comment blocks to the top of the files, describing what, when, whys etc of the file, so that whenever a new developer goes through the code, it will be more readable and he/she can get started with code easily and quickly. To automate this process I created the JS File header extension, which on activating will add a comment block to the top of your file and you can update the content. It also automatically adds the author details, created at and last modified at information (which is updated whenever you save the file).

![My First VS Code Extension](https://cdn.hashnode.com/res/hashnode/image/upload/v1682041029850/49332b9f-ecb4-45db-a08c-c504a2d386cf.gif align="left")

Its published on the VS Code marketplace and available for download, you can download it here: [marketplace.visualstudio.com/items?itemName..](https://hashnode.com/util/redirect?url=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Darjunkomath.js-file-header&ref=techulus.xyz)

If you feel like contributing to the project, I’m more than welcome, checkout the code in github: [github.com/arjunkomath/js-file-header-vscode](https://hashnode.com/util/redirect?url=https%3A%2F%2Fgithub.com%2Farjunkomath%2Fjs-file-header-vscode&ref=techulus.xyz)