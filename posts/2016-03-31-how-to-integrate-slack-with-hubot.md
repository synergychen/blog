---
layout: post
title: How to Integrate Slack With Hubot
date: 2016-03-31 16:19:03
categories: Tools
---

> Hubot + Slack = Work Automation

### Prerequisite
Node.js and heroku are required:

{% highlight bash %}
brew install node
brew install heroku-toolbelt
{% endhighlight %}

### Create a new bot
{% highlight bash %}
npm install -g hubot coffee-script yo generator-hubot
mkdir -p /path/to/hubot
cd /path/to/hubot
yo hubot
npm install hubot-slack --save
{% endhighlight %}

When asked about `Bot Adaptor`, you could leave it as `Campfire` for now.

### Initialize git and commit
{% highlight bash %}
git init
git add .
git commit -am "<commit-message>"
{% endhighlight %}

### Configure hubot on Slack
Search for [hubot](https://slack.com/apps/search?q=hubot) on slack and install.

After get slack API, run following
{% highlight bash %}
HUBOT_SLACK_TOKEN=<YOUR_SLACK_API_TOKEN_HERE> ./bin/hubot --adapter slack
{% endhighlight %}

Now you could go to slack app and chat with your robot. e.g. send a message `pug me`.

Up to now, hubot-slack works on your local, following is how to deploy it to
heroku, in order to keep your robot be on almost all the time.

### Change bot to point to Slack
Open `Procfile`, make sure you have:

{% highlight bash %}
web: bin/hubot -a slack -n hubot
{% endhighlight %}

### Make your bot always online: Deploy to heroku

{% highlight bash %}
heroku create <name-of-your-robot>
heroku addons:create rediscloud:30
heroku config:add HEROKU_URL=https://<your-bot-app-name>.herokuapp.com
heroku config:add HUBOT_SLACK_TOKEN=<YOUR_TOKEN_HERE>
git push heroku master
{% endhighlight %}

### Keep hubot alive
A free Heroku dyno can only run for 18 hours/day, so we'd better let our bot sleep when we sleep.

{% highlight bash %}
npm install hubot-heroku-keepalive --save
{% endhighlight %}

And make sure your have `"hubot-heroku-keepalive"` in `external-scripts.json`.

Then configure heroku config, where `PASTE_WEB_URL_HERE` is from `Web URL` of `heroku apps:info`.

{% highlight bash %}
heroku config:set HUBOT_HEROKU_KEEPALIVE_URL=PASTE_WEB_URL_HERE
{% endhighlight %}

Hubot is set. However, it needs a trigger to initial start everyday, that's why
we use [Heroku Scheduler](https://devcenter.heroku.com/articles/scheduler)

{% highlight bash %}
heroku addons:create scheduler:standard
{% endhighlight %}

Then open scheduler UI by run

{% highlight bash %}
heroku addons:open scheduler
{% endhighlight %}

And configure it with

{% highlight bash %}
curl ${HUBOT_HEROKU_KEEPALIVE_URL}heroku/keepalive
{% endhighlight %}

Notice *NEXT DUE* is UTC based.

If you got further issues with heroku, you could always access to config and
logs to see more details.

### Check Heroku config
In order to see hubot config on Heroku, run

{% highlight bash %}
heroku config
{% endhighlight %}

### Debug Heroku if your bot is offline
Sometimes bot on Heroku in awake while offline on Slack, to double check the status and logs, run

{% highlight bash %}
heroku ps
heroku logs
{% endhighlight %}
