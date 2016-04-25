---
layout: post
title: To clone or not to clone? (Part 1)
---

A few days ago I was debugging an issue in one web application.   
All tracks were pointing to Java Script logic that shortly speaking was creating a copy of the array and then modifying the destination array.  

# Problem
Check out the code below. I must say I wasn't expecting the result I saw.
{% highlight javascript linenos %}
    var alphabet = ['a', 'b', 'c'];
    var newAlphabet = source;
    destination.push('d');

    console.log(alphabet);
    console.log(newAlphabet);
{% endhighlight %}
Surprisingly for me the output was:
{% highlight javascript %}
    ["a", "b", "c", "d"]
    ["a", "b", "c", "d"]
{% endhighlight %}

Wait a minute. Wasnt't I just modifying destination array?   
Not really. Turns out that:
{% highlight javascript %}
    var newAlphabet = alphabet;
{% endhighlight %}

is treated as setting newAlphabet with a reference to alphabet array.
NewAlphabet array is never created/copied.
**That way modifying newAlphabet variable was modifying alphabet array.**

# Solution
In order to achive my goal I needed to somehow clone the array content.
After googling around I found out that answer to that question was not that trivial.
One of the most often given solutions was to use JavaScript [slice](https://developer.mozilla.org/docs/Web/JavaScript/Referencje/Obiekty/Array/slice) function:

{% highlight javascript linenos %}
    var alphabet = ['a', 'b', 'c'];
    var newAlphabet = source.slice();
{% endhighlight %}
 
The function was giving correct results. I was more then happy to fix that bug.
 
However I started to think if it is also going to work with more complex arrays...

I will try to tell you more about my findings in next part of that post.

Stay tuned :)