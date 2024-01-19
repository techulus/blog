---
template: post
title: "Free website monitoring with instant push notification alerts"
date_published: 1581377243000
cover: /cover/servers.jpeg
---

In this article, I’ll help you set up a free and simple website monitoring tool which sends instant alerts using push notification. Before we begin, let’s have a look a what we will need:

* a website URL to test, obviously
    
* a computer/server to run our bash script
    
* a free account at [push.techulus.com](https://push.techulus.com/?ref=techulus.xyz), we will be using [Push by Techulus](https://push.techulus.com/?ref=techulus.xyz) for delivering real-time push notifications.
    

What is a website monitoring service? It’s simply a tool that lets us check if our website/server is live or not and also send us instant alerts the moment our website/server goes down. There are many SaaS platform which has several other advanced features, but in this tutorial, we will keep things simple.

Before we start, make sure you’ve set up your account at [push.techulus.com](https://push.techulus.com/?ref=techulus.xyz), installed the app on your device and copied the API key.

![Free website monitoring with instant push notification alerts](/images/push/web.jpeg)

Get the API key from Push console

Here is the bash script we will be using. You’ve to make two changes:

* change the website URL in the script to the one you want to monitor
    
* Update the file with API key from [push.techulus.com](https://push.techulus.com/?ref=techulus.xyz)
    
    ```bash
    #!/bin/bash
    # This script will check to see if a website is up/down by pinging the url
    # your url 
    url="http://blahblahblah.com"
    # your api key from https://push.techulus.com/ 
    push_api_key=""
    # push settings 
    sendNotification(){
     curl -X "POST" "https://push.techulus.com/api/v1/notify/${push_api_key}" \
      -H 'Content-Type: application/json; charset=utf-8' \
      -d "{
     \"title\": \" $1 \",
     \"body\": \" $2 \"
    }"
    }
    # check url 
    wget --server-response --spider --tries=3 $url
    # This wget will only return exit 0 if response is 200 ok
    if [ "$?" -eq 0 ] # so if we have exit status of zero then server is UP
    then
     exit 0
    else
     echo "DOWN | `date`"
     sendNotification "$url is DOWN" "DOWN | `date`"
     exit 0
    fi
    ```
    

All you need to do is, download this script into your machine or server and keep running this script in a regular interval using something like cronjob and we’re done! That’s it! 🥳

The script tries to load our website and if it fails (the server doesn’t respond with status code 200 OK), we assume that something has gone wrong and trigger a push notification.

![Free website monitoring with instant push notification alerts](/images/push/notification.jpeg)

Make sure you run this script frequently so that we can be alerted on time. To run this script every minute using *cronjob*, we can add the following command to *crontab*. Open crontab using the command

`crontab -e`

and then add the following line:

`/bin/bash /path_to_your_file/script.sh`

Make sure that you add the correct and absolute path to the script file on your machine/server.

Feel free to modify the script, maybe change the message to make it more meaningful or more contextual. Before I wrap this up, huge shoutout to [vbarrier](https://gist.github.com/vbarrier/4d28d71ee8227d8a80cc6c1d57f46702?ref=techulus.xyz). The bash script I’m using here is a modified version of [his script](https://gist.github.com/vbarrier/4d28d71ee8227d8a80cc6c1d57f46702?ref=techulus.xyz).

Feel free to leave comments in case you have any questions.

Thank you!