---
template: post
title: "How to: Get push notifications from GitHub"
date_published: 1573428443000
cover: /cover/phone-notifications.jpeg
amp: true
---

If you’ve got a mobile phone, then you probably know what push notifications are. A [push notification](https://www.twilio.com/docs/glossary/what-is-push-notification?ref=techulus.xyz) (also known as a server push notification) is the delivery of information to a computing device from an application server where the request for the transaction is started by the server rather than by an explicit request from the client. Basically, it’s these bubbles that pop up on your device.

> **We will use Push (**[**push.techulus.com**](https://push.techulus.com/?ref=techulus.xyz)**) as the medium for receiving push notifications.**

In this article, we’ll be discussing how we can get notifications from GitHub as push notifications on our device.

### Let’s get started

We will setup a real-time push notification workflow using [GitHub actions](https://github.com/marketplace/actions/send-push-notification?ref=techulus.xyz) (FYI, we could do the same using [Zapier integration](https://zapier.com/platform/public-invite/7743/eacfd29c4087cb67e7798c9876698682/?ref=techulus.xyz) also). Before we start, make sure you’ve setup your account at [push.techulus.com](https://push.techulus.com/?ref=techulus.xyz), installed the app on your device and copied the API key.

![How to: Get push notifications from GitHub](/images/push/web.jpeg)

Get the API key from Push console.

Now that we have everything ready, let’s create our workflow on GitHub. We will create a workflow that sends a push notification whenever there is a new issue in our repository.

**Step 1.** Open your GitHub repository page (I will use this repository [https://github.com/arjunkomath/ama](https://github.com/arjunkomath/ama?ref=techulus.xyz)) and go to **Actions** page.

![How to: Get push notifications from GitHub](/images/ama/arjun.png)

**Step 2.** To create a new workflow click on “New workflow” or “Set up a workflow yourself” button. Now GitHub will draft a new workflow for you with an `echo Hello, world!` command. Let’s change this and add our custom action.

**Step 3.** Rename the file to `issues_push.yml` and then paste the following into your editor.

```yaml
name: Notify issues

on: issues: types: [opened]

jobs: push:

runs-on: ubuntu-latest

steps: - name: Send Push Notification uses: techulus/push-github-action@v0.0.2 env: API_KEY: ${{ secrets.PUSH_API_KEY }} MESSAGE: "There is a new issue 😅"
```

Let’s go through the lines one by one:

* The first line defines the `name` of this workflow
    
* The second line specify the trigger for this workflow, in our case it is when a new issue is opened
    
* Next we have defined a job `push` that runs on `ubuntu-latest` , the [virtual environment](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/virtual-environments-for-github-hosted-runners?ref=techulus.xyz) in which our workflow commands will be executed.
    
* Finally, we have the steps for the workflow which is to send the actual notification. We will use [Send Push Notification](https://github.com/marketplace/actions/send-push-notification?ref=techulus.xyz) action that has been published to GitHub marketplace.
    
* Below that we’ve specified our `API_KEY` as a secret and at last the message for our notification. We will see how to create a secret in a moment.
    

Commit this file to master and we have created our workflow! 🎉

**Step 4.** Before testing the notification we have to create a secret to store our `API_KEY` . Open your repository settings and go to secrets tab and then click on **Add a new secret.**

![How to: Get push notifications from GitHub](/images/ama/secrets.png)

### **Add a new secret**

Enter the name as `PUSH_API_KEY` (we specified this in our workflow using `secrets.PUSH_API_KEY` ) and enter the API key you copied from push console as the value. Click on **Add secret** and we’re done!

![How to: Get push notifications from GitHub](/images/ama/secrets_2.png)

Time to test our workflow, create a new issue in your repository and momentarily you should get the notification on your device.

![How to: Get push notifications from GitHub](/images/ama/notification.png)

We can reuse the same action to implement different notifications based on different triggers. You can find more examples on the marketplace page [https://github.com/marketplace/actions/send-push-notification](https://github.com/marketplace/actions/send-push-notification?ref=techulus.xyz).

Feel free to leave comments in case you have any questions.

Thank you!