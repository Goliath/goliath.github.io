---
layout: post
title: Grails - get sessionFactory instance when having multiply data sources
---

Everyone knows how to inject bean for a given data source, but what about sessionFactory?

Injecting data source could look like this:
{% highlight groovy linenos %}
   def dataSource_other
{% endhighlight %}



where dataSource_other is the registered dataSource object.

# Problem
What about accessing certain sessionFactory object when having multiply data sources?

# Solution

Turns out that certain sessionFactory can be injected like data source:
 
Code below:
{% highlight groovy linenos %}
    def sessionFactory_foo
{% endhighlight %}

where dataSource_foo would be the name of the data source.


