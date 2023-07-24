---
template: post
title: "How I Built a Serverless API to Optimize User-Uploaded Images on the Fly"
datePublished: Thu Apr 20 2023 09:46:56 GMT+0000 (Coordinated Universal Time)
featured: true
cover: https://images.unsplash.com/photo-1581092918056-0c4c3acd3789?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxMTc3M3wwfDF8c2VhcmNofDl8fGZpeHxlbnwwfHx8fDE2ODE5ODU1NjQ&ixlib=rb-4.0.3&q=80&w=2000
---

Optimizing images for the web is a crucial step in improving the performance and user experience of a website. However, it can be challenging to optimize user-uploaded images when you don't know their dimensions in advance. This is where server-side image processing comes in handy.

In this blog post, we'll walk through the process of building a serverless API that resizes images on the fly, ensuring that they are always smaller than the max view width of 624 pixels.

To accomplish this, we'll be using Next.js, and the sharp image processing library. Let's get started!

## Setting up the API

First, we need to set up a new API route in our Next.js application. In this example, I created a new file in the `pages/api/render` directory called `image.ts`. This file will contain the code to resize the image.

Next, we need to install the `sharp` library. Open up your terminal and run `npm install sharp`.

## Resizing the Image

Now that we have our API route set up and the sharp library installed, we can start resizing our images. Here's the code to resize the image:

```typescript
import { createHash } from "crypto";
import type { NextApiRequest, NextApiResponse } from "next";
import sharp from "sharp";

async function renderImage(req: NextApiRequest, res: NextApiResponse<Buffer>) {
  const imageUrl = req.query.url as string;

  // Fetch image from url using fetch
  const imageBuf = await fetch(imageUrl).then(async (res) =>
    Buffer.from(await res.arrayBuffer())
  );

  const imageMetadata = await sharp(imageBuf).metadata();

  const image = await sharp(imageBuf)
    .resize({ width: Math.min(imageMetadata?.width || 624, 624) })
    .toFormat("png")
    .png({ quality: 80 })
    .toBuffer();

  res.setHeader("Content-Type", "image/png");
  res.setHeader("Cache-Control", "public, max-age=31536000, immutable");
  res.setHeader("ETag", `"${createHash("md5").update(image).digest("hex")}"`);

  res.send(image);
}

export default renderImage;
```

Let's break down the code. First, we retrieve the URL of the image we want to resize from the query parameter. Then, we use the `fetch` API to retrieve the image from the URL and convert it to a buffer.

Next, we use the `sharp` library to retrieve the metadata of the image. We use this metadata to determine the width of the image. We then use the `resize` method to resize the image to a width that is the minimum of the original width or 624 pixels.

We then convert the resized image to the PNG format and set the quality to 80. Finally, we set the headers of the response to indicate that it is a PNG image, that it can be cached for a year, and that it has an ETag based on the MD5 hash of the image. We then send the image buffer as the response.

And that's it! With this API route in place, any image that is requested from this route will be resized to a width that is the minimum of the original width or 624 pixels, ensuring that it is optimised for the web.