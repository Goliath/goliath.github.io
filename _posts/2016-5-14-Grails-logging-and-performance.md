---
layout: post
title: Grails logging and performance
---

"The deeper level of logs is, the less often it will be logged" - we use to say.
Well that's not true.

# Problem

Take an example with grails log.debug call.

Let's say I want to log a very often executed code.
{% highlight groovy linenos %}
    Long sum = 0
    (1..1000).each { number ->
        ++sum
        log.debug "Sum = ${sum}"
    }
{% endhighlight %}

I use log.debug so my information is logged only if my project configuration allows that.
That way if we turn off DEBUG the logged line should not affect application speed.
But is that really true?

Let's check if the logged value is really accessed?  
We need to turn off DEBUG and execute following code:  

{% highlight groovy linenos %}
    Long sum = 0
    (1..1000).each { number ->
        log.debug "Sum = ${++sum}"
    }
{% endhighlight %}

Well, after finishing the loop, sum value is 1000, it was incremented even when information was not logged. 
That means that every time you log heavy operations like e.g. object.dump() it will get executed, even if the log level is not suppose to show that line.

# Solution

Possible solution is to add condition before logging.

{% highlight groovy linenos %}
    Long sum = 0
    (1..1000).each { number ->
        if (log.debugEnabled) {
            log.debug "Sum = ${++sum}"
        }
    }
{% endhighlight %}


# Sum up

Turns out that logged value is accessed even when information is not logged.  
Keep that in mind since it may not only bring down performance of your application, it may be even a reason of a bug.
