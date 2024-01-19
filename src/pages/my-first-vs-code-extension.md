---
template: post
title: "My First VS Code Extension"
date_published: 1525912043000
cover: /images/js_file_header.png
---

> Finally, after playing around with VS Code a lot, I decided I should publish a plugin. I had a few ideas in mind, mostly minor helpers that would help me in my work.

I started off with a simple yet useful extension. I work with Javascript code every day, it could be React or NodeJS, mostly microservices build on AWS Lambda. I used to manually add comment blocks to the top of the files, describing what, when, whys etc of the file, so that whenever a new developer goes through the code, it will be more readable and he/she can get started with code easily and quickly. To automate this process I created the JS File header extension, which on activating will add a comment block to the top of your file and you can update the content. It also automatically adds the author details, created at and last modified at information (which is updated whenever you save the file).

![My First VS Code Extension](/images/js_header_demo.gif)

Its published on the VS Code marketplace and available for download, you can download it here: [marketplace.visualstudio.com/items?itemName..](https://marketplace.visualstudio.com/items?itemName=arjunkomath.js-file-header)

If you feel like contributing to the project, I’m more than welcome, checkout the code in github: [github.com/arjunkomath/js-file-header-vscode](https://github.com/arjunkomath/js-file-header-vscode)