---
title: Split HTTP Request Into Pieces
date: 2014-09-24 16:54:51
layout: post
categories: Web
---

> Human unreadable, that's my first impression of HTTP. Let's split it into pieces.

### HTTP content

When you input google.com in address bar and press enter, essentially, what you do is sending a request to Google, letting google return all the content of the website and displaying it on your web browser. But what's really in that response content?

Basically it contains two parts: header and message body. Here is a picture showing the http content using `http` command, which could be installed with

{% highlight bash %}
brew install httpie
{% endhighlight %}

{% highlight bash %}
HTTP/1.1 301 Moved Permanently
Cache-Control: public, max-age=2592000
Content-Length: 219
Content-Type: text/html; charset=UTF-8
Date: Mon, 18 Jan 2016 16:41:12 GMT
Expires: Wed, 17 Feb 2016 16:41:12 GMT
Location: http://www.google.com/
Server: gws
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
{% endhighlight %}

### HTTP header

To http beginners like me, there are two things we should know:
- header includes HTTP status code in first line.
- there is a blank line right after header.

#### HTTP status code

When you are trying to open a website, most of time, it would return the website as you want. However, sometime it returns an error like **404 Not Found**, meaning that the website or resources you requested can't be found, probably the server crashes.

Here are some common HTTP status codes

| status code | description |
| ----------- | ----------- |
| 200 | request succeeded |
| 301 | request redirected to another url |
| 400 | request could not be understood by server due to bad syntax |
| 401 | request unauthorized; usually due to failed login |
| 404 | requested resources could not be found |
| 500 | server encounters internal errors |

To see more status code with a brief description, visit [here](http://httpstatus.es/ "httpstatus").

### HTTP message body

The structure of the message body is composed of two parts: HEAD and BODY.

#### HTTP methods

Analogy is how we understand things better. The following table is showing four basic http methods and comparing it to other methods like real world methods and SQL methods.

| http world | SQL | real world |
| ---------- | --- | ---------- |
| GET | SELECT | read |
| PUT/PATCH | UPDATE | update |
| POST | INSERT | create/new |
| DELETE | DELETE | delete |
