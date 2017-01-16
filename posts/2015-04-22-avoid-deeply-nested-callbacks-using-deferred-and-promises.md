---
title: Avoid Deeply Nested Callbacks Using Deferred and Promises
date: 2015-04-22T13:24:04+00:00
layout: post
categories: JavaScript
---
> Do it later. I am promise.

If you are an Ajax beginner, you might do

{% highlight javascript %}
$.ajax({
  method: "GET",
  url: "/page/index",
  success: successFunction,
  error: errorFunction
});
{% endhighlight %}

It works but the problem is `.success` and `.error` methods are used prior to jQuery 1.5 and it always make your JavaScript code quite long and nested if you have a few `callbacks` inside your `success` or `error` function.

### List of content

1. done / fail / always
2. then ( pipe )
3. when
4. $.Deferred and promises

### .done/.fail/.always

Programmers love simple individual blocks. So let's extract `success`, `fail` and `callbacks` from Ajax using `.done`, `.fail`, `.always` first.

`.always` would executed either done or fail.

{% highlight javascript %}
var req = $.ajax({
  method: "GET",
  url: "/page/index"
});

req.done(successFunction);
req.fail(errorFunction);
req.always(alwaysFunction);
{% endhighlight %}

### .then (.pipe)

Another nice feature is `.then`, which is equivalent to `.done` + `.fail`.

`.then` could take one or two argument. It would ignore failure case if only one argument is given.

{% highlight javascript %}
var req = $.ajax({
  method: "GET",
  url: "/page/index"
});

req.then(successFunction, errorFunction);
req.then(successFunction);
{% endhighlight %}

`.then` could be chained. In the following case, if `req1` fails, then `req3` will be called, then if `req3` success, `req4` will be called.

{% highlight javascript %}
var req1 = $.ajax("/page/1");
var req2 = $.ajax("/page/2");
var req3 = $.ajax("/page/3");
var req4 = $.ajax("/page/4");
var req5 = $.ajax("/page/5");

req1.then(req2, req3).then(req4, req5);
{% endhighlight %}

What about pipe and when should I use it? In theory, pipe = then. However, pipe is deprecated in jQuery 1.8. So answer is **Forget about pipe. Use then instead**.

### .when

We could look it as chaining two `.then` with AND logic, meaning that both events should succeed to trigger success function. In the following case, `successFunction` will be called only if both `req1` and `req2` succeed, otherwise, `errorFunction` will be called.

{% highlight javascript %}
var req1 = $.ajax("/page/1");
var req2 = $.ajax("/page/2");

$.when(req1, req2).then(successFunction, errorFunction);
{% endhighlight %}

### $.Deferred and promises

By creating Deferred object, we are able to set up our own deferred processes, which would reduce deeply nested callbacks.

{% highlight javascript %}
// create deferred object
var dfd = $.Deferred();

dfd.done(function(resp){ console.log(resp) });

dfd.resolve("Hello");
{% endhighlight %}

For practical situations, we use deferred in user defined asynchronous functions as follows. Comments show timing order of steps.

{% highlight javascript %}
var promise = userAsync();            // step 1

promise.done(function(){
  console.log("Promise resolving")    // step 5
});

function userAsync(){
  var dfd = $.Deferred();             // step 2

  setTimeout(function(){
    console.log("Before resolving");  // step 3
    dfd.resolve();                    // step 4
    console.log("After resolved");    // step 6
  }, 1000);

  return dfd.promise();
}
{% endhighlight %}

The output is

{% highlight javascript %}
> Before resolving
> Promise resolving
> After resolved
{% endhighlight %}

Let's have a more complicated case with a user defined function being either async or sync service. In this case, when `num === 1`, `maybeAsyncService` is `async`, otherwise, it's `sync`.

{% highlight javascript %}
function maybeAsync(service){
  var dfd = $.Deferred();

  if ( service === "async" ) {
    setTimeout(function(){
      console.log("Before resolving");            // step 3
      dfd.resolve(service);                       // step 4
      console.log("After resolved");              // step 7
    }, 1000)

    return dfd.promise();
  } else {
      console.log("Sync service")                 // step 2
      return service;
  }
}

$.when(maybeAsync("async"), maybeAsync("sync"))   // step 1
  .then(function(response1, response2){
    console.log(response1);                       // step 5
    console.log(response2);                       // step 6
  });
{% endhighlight %}

In this case, timing would be

Step 1. both `maybeAsync("async")` and `maybeAsync("sync")` start
Step 2. **Sync service** prints, then waiting async service to finish
Step 3. one second later, **Before resolving** prints in async service
Step 4. `dfd` start to resolve
Step 5. `async` prints since both two service succeed
Step 6. `sync` prints since both two service succeed
Step 7: **After resolved** prints

And output is

{% highlight javascript %}
> Sync service
> Before resolving
> async
> sync
> After resolved
{% endhighlight %}
