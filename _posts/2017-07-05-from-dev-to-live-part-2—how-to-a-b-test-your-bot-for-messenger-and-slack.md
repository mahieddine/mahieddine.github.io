---
layout: post
title:  "From Dev to Live : Part 2 — How to A/B test your bot for Messenger & Slack."
date:   2017-07-05 20:00:23 +0700
categories: [ai]
comments: true
---

![cover](/static/img/upload/from-dev-to-live-part-2—how-to-a-b-test-your-bot-for-messenger-and-slack/cover.png?:xl:)

Split testing, also known as A/B testing, is used commonly to compare two versions of a website or app and measure performance of each one regarding some quantifiable goal to decide which one performs better. This is fairly simple to put in place for a website or an app thanks to the many great tools out there, but when it comes to bots there is not a tool for that.

In this tutorial, I will show you how you can split your users into two groups, and serve them two versions of your bot.

In order to keep it simple, we are going to stick with our very simple [nodejs echobot](https://github.com/mahieddine/echobot) (it’s a bot that just echoes back everything your type on Messenger), and we also created another version of this same bot except that in this version we send an animated GIF too, we will call that bot echobot-v2.

So let’s get started, go on your server, and clone these two github repositories, edit the “app.js” file, and set your fb access token and also your fb app’s secret key.

```Shell
# clone & setup the version A
git clone https://github.com/mahieddine/echobot && cd echobot && npm install
# open app.js file and put in there your page access token and your fb app secret key
cd ..
# clone & setup the version B
git clone https://github.com/mahieddine/echobot-v2 && cd echobot-v2 && npm install
# open app.js file and put in there your page access token and your fb app secret key
cd .. 
# launch the A bot version (A listens on 3000)
cd echobot && node app.js &
# >>facebook webhook running on localhost:3000/webhook
# launch the B bot version (B listens on 4000)
cd echobot-v2 && node app.js &
# >>facebook webhook running on localhost:4000/webhook
```

Now we have our two bot instances up & running on our server.

You can login on [MachinaBot](https://machinabot.com/) (if you are not a member yet ask for an invite here and tell us that you are coming from Medium 🤠 so you will be invited quickly 🐥)

Once logged, go to your app’s router page and declare your two bots instances (and don’t forget to enable them!).

![add nodes](/static/img/upload/from-dev-to-live-part-2—how-to-a-b-test-your-bot-for-messenger-and-slack/add_nodes.gif?:xl:)

Now that we declared our two bot instances (version A & B), click on the routing strategies tab

![add nodes](/static/img/upload/from-dev-to-live-part-2—how-to-a-b-test-your-bot-for-messenger-and-slack/routing_strategies.gif?:left:s:rspace:)

Choose the **“Round Robin”** routing strategy (which should be already selected since it’s the default one) and also turn on **“sticky session”** option. This will make the router split your users into 2 groups, 50% of them will be routed & served by the version A of your bot and the other 50% will be served by the version B of your bot.

Note that this is an A/B testing on the bot level (we are using two different bot instances) but you can also of course do A/B testing on a message per message basis, this can be achieved easily by declaring your same bot instance two times in the router but with additional parameters that will make your bot picks the version A or B of a message for example.

```Shell
https://MY_SERVER_HOSTNAME:3000/webhook?v=A
https://MY_SERVER_HOSTNAME:3000/webhook?v=B
```
If your bot was already plugged on MachinaBot that was all you had to do to setup A/B testing, but if it’s not the case then there is one last task to perform which is obviously to create a channel on MachinaBot, so we can relay your Facebook/Slack webhooks activity to your bot.

To do so, go in the integration page, and create a new channel, give it a nice name, select your messaging platform and hit create, next set your HMAC SHA 1 secret key to protect your webhook endpoint from unauthorized access.

![add nodes](/static/img/upload/from-dev-to-live-part-2—how-to-a-b-test-your-bot-for-messenger-and-slack/integration.gif?:xl:)

Now go to [https://developers.facebook.com/apps/{YOUR FB APP ID}/webhooks](https://developers.facebook.com/apps/{YOUR FB APP ID}/webhooks), and edit/create your facebook app webhook’s subscription, you should make it point to your MachinaBot **inbound** endpoint. To do that click on the inbound endpoint tab and copy/paste your inbound webhook URL and also your facebook verification token into your facebook app webhooks settings.**+Click** on verify and Save.

That’s it. You can try to send messages to your bot with two different Facebook/Slack accounts and what you will see is that every user will be served by version A or B of your bot.


