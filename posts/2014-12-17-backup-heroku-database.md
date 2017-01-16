---
title: Backup Heroku Database
date: 2014-12-17T18:14:16+00:00
layout: post
categories: Heroku
---

> We are about to open time capsule in Heroku. Please fasten your seat belt.

You would have risk of crash database in Heroku if you change the database and migrate to Heroku.

In order to avoid data loss, it's better and never be wrong to backup your Heroku database.

Make sure you are in the right directory of your Rails app before Heroku database operations.

### Create a backup

This would create a new backup on Heroku.

{% highlight bash %}
heroku pgbackups:capture
{% endhighlight %}

### List all backups

{% highlight bash %}
heroku pgbackups
{% endhighlight %}

### Delete a backup

{% highlight bash %}
heroku pgbackups:destroy b001
{% endhighlight %}

where `b001` is the database backup version number.

### Restore a backup

DATABASE_URL is exactly what it is, you don't need to replace it with anything else.

{% highlight bash %}
heroku pgbackups:restore DATABASE_URL b004
{% endhighlight %}
