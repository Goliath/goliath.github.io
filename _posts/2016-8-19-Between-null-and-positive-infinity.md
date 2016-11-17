---
layout: post
title: Between null and positive infinity
---

A funny null fact I found out after so many years of working with  groovy.

# Problem
I happen to create a construction like this: 

{% highlight groovy linenos %}
     if(object?.value > 0) {
        println "did something"        
     } else {
         println "did nothing"
     }
{% endhighlight %}
Are you sure what will be printed **when object is null**?   
I must say I wasn't.  

We got used to negate null in groovy like this:   
{% highlight groovy %}
    assert !null == true   
{% endhighlight %}   

but what about using null with relation operator?  

# Turns out 
 
All this below will execute: 
{% highlight groovy linenos %}
    assert null < 0   
    assert null < Integer.MIN_VALUE
    assert null < Double.NEGATIVE_INFINITY
{% endhighlight %}

so lets remember..
**null is the lower then anything.** 

