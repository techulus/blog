---
template: post
title: "Authenticating Vercel Cron Jobs"
date_published: 1707568444408
amp: true
---

Vercel Cron Jobs are a powerful tool for automating repetitive tasks. By using cron expressions, you can schedule tasks to run automatically at specific intervals. However, securing these cron jobs is crucial to ensure that they can't be run by just anyone with the known route.

Here's a step-by-step guide on how to authenticate Vercel Cron Jobs:
- **Create a Secret Key**: Use the `openssl rand -hex 32` command in your terminal to generate a secret key.
- **Add the Secret Key to Your Environment Variables**: Add the CRON_SECRET variable to your local .env file with the value generated from the previous step.
- **Modify Your Cron Job Route**: Look for the bearer token in your cron job route. If it doesn't exist or if it doesn't match the CRON_SECRET, return an unauthorized response with a 401 status code.

```ts
import { NextRequest, NextResponse } from 'next/server'

export async function GET(req: NextRequest) {
  // get the bearer token from the header
  const authToken = (req.headers.get('authorization') || '')
    .split('Bearer ')
    .at(1)

  // if not found OR the bearer token does NOT equal the CRON_SECRET
  if (!authToken || authToken != process.env.CRON_SECRET) {
    return NextResponse.json(
      { error: 'Unauthorized' },
      { status: 401 }
    )
  }

  // if token exists then move on with the cron job ...
}
```

- **Add the Secret Key to Your Vercel Project Settings**: Add the CRON_SECRET variable to the Vercel project settings Environment Variables.
- **Test Your Setup**: Deploy your project to Vercel and test on your live site. You should receive an error message "Unauthorized" if the setup is correct. Next, try triggering the cron job from Vercel dashboard, it should run as expected.

By following these steps, you can ensure that only Vercel can run the cron job from their servers.

