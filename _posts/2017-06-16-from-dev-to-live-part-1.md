---
layout: post
title:  "From Dev to Live : Part 1 — How to start testing and debugging your bot locally in one minute  (Hassle-free guarantee)"
date:   2017-06-16 20:00:23 +0700
categories: [ai]
---

![](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/cover.png?:center:xl:)

Creating a bot is relatively easy, but wouldn’t be great if you were able to test your bot on localhost, work with your team mates, and debug your bot easily in one place ?

MachinaBot local relay feature let’s you do all of that in no-time.

+ An up and running chatbot instance on your local machine, if it’s not the case you can pick our Messenger echo bot sample from Github (it’s a Messenger chatbot that just echoes back everything you type)
+ Go to machinabot.com and sign-in (if you don’t have an account yet, ask for an invite and tell us that you are coming from Medium so you will get in faster 😎).

Everything is ready ? So let’s get started
This is what we’ll cover in this tutorial:

+ What is MachinaBot ?
+ Local testing : Test your bot on localhost.
+ Team collaboration: How you can work on your bot with your team mates without having to create a Facebook page/Slack team…whatever for every developer 😜.

By the end of this tutorial you will master how MachinaBot works and how you can take advantage of it in your bot development process.

Usually your bot receives a webhook notification from your messaging platform (Messenger, Slack…), at least every time an user sends a message to your bot. However webhooks are always a little more complicated to put in place, monitor, debug, and scale especially in messaging context, and this is when MachinaBot comes into play. MachinaBot is a relay gateway which means it relays your messages from and to your bot, this enables MachinaBot to offer you all kind of cool stuff like technical monitoring, A/B testing, routing mechanisms and much more.

![](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/overview.gif?:center:l:)

To do that we need to do two things :

+ Create an integration endpoint to capture all your messaging platform’s webhooks.
+ Secondly add the MachinaBot client chrome extension.

So let’s start by creating our first channel, on the left side menu **+Click** on Integration, then **+Click** on New channel

Give your channel a meaningful name (like your facebook page/slack team…name), select your messaging platform and **+Click** on create

Congrats ! you just created your first channel

A channel has two endpoints, an **inbound** one for messages coming **from** your messaging platform (Messenger, Slack…) to your bot.

![inbound](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/inbound.png?:center:s:)

And an **outbound** endpoint for messages **going from** your bot **to** messaging platform.

![outbound](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/outbound.png?:center:s:)

Since our bot sample is a Messenger bot, we need to check the HMAC SHA1 signature of our webhooks, to do so click on HMAC SHA 1 and put there your [Facebook app secret key](https://stackoverflow.com/questions/3203649/where-can-i-find-my-facebook-application-id-and-secret-key) then **+Click** on update

![integration](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/integration.gif)

Perfect, our inbound endpoint is configured and secured.

We can now go to [https://developers.facebook.com/apps/{appid}/webhooks](https://developers.facebook.com/apps/{appid}/webhooks), and edit/create our webhook subscription we should make it point to our MachinaBot **inbound** endpoint. So go to the inbound endpoint tab and copy/paste in the facebook subscription form your inbound webhook URL and also your facebook verification token.**+Click** on verify and Save.

Now go to the local relay page, and install the MachinaBot client chrome extension.

![chrome extension](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/chrome_extension.gif?:xl:)

All you have to do now is to **+Click** on the “Relay webhooks to localhost” button, fill in your local bot instance url (in our sample it’s : [http://localhost:3000/webhook](http://localhost:3000/webhook)), and hit start.

![local relay](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/local_server.gif?:xl:)

If you send a message to your facebook bot’s page, it will be relayed directly to your local bot instance.

![relay](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/relay.gif?:xl:)

And of course you can also check your wehooks details, replay them…etc by clicking on the eye button.

Great, isn’t it ?

![webhook call details](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/webhook_details.png?:left:s:rspace:)

When you develop your bot app you need to test it, thanks to MachinaBot local relay feature you can do that easily, but what if you are two or more developers working on the same bot and you don’t want to bother your mates ? the current work around is that every developer creates his own test facebook page or slack team… right? we are going to see how you can use only one Facebook page or slack team for all your developers 💪.

In MachinaBot an app is a logical container that encapsulates all your bot’s nodes, routing strategies, integration channels, webhooks logs. Hence all you have to do is create a team, select the app you want to share with your mates and hit create.

![create team](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/create_team.gif?:xl:)

Then invite your mates on the team you just created

![create team](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/teams_and_permission.gif?:xl:)



Come back to your local relay page, and **+Click** on “Relay your webhooks to localhost”, we are going to leverage the filter messages feature to achieve what we want namely every developer should only receive his own messages on the local bot instance.

![create team](/static/img/upload/from-dev-to-live-part-1—how-to-start-testing-and-debugging-your-bot-locally-in-one-minute/local_server_2.png?:left:s:rspace:)

The filter messages feature is mainly based on the powerful [JS Path library](https://github.com/dfilatov/jspath), it enables you to filter out the messages you want to relay on your local machine. In our case every developer wants to receive only the messages he sent to the Facebook test team page.

So basically we need to set a filter on the sender.id field, to do that, copy the sample expression already provided (‘{“object”:”page”,”entry”:{“id”:**1617683738452256**,”messaging”:’ ++ .entry.messaging{.sender.id==**1064642320272438**} ++ ‘}}’) in the “Filter messages” field, replace sender.id value with your Facebook’s page-scoped user id (you can check the logs to get it), and also update entry.id with your facebook’s page id.  


Now hit start and that’s it. Every developer can message the facebook team test page and yet only receives his own message on his local bot instance.



