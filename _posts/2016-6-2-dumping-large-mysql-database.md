---
layout: post
title: Dumping large MySQL database
---

During some troubleshooting on one of projects I needed to get latest dump from remote mysql database server I couldn't ssh to.  
Easy thing... but the database was actually quite huge...

{% highlight bash %}
mysqldump database > database_dump.sql
{% endhighlight %}

# Problem

Dump file size was ~3GB which might take quite long. Especially when the connection to mysql server was not fast enough.  

# Solution

After a few attempts and noticing that it might take too long to fetch all data I found out that there is a nice switch in mysql and mysqldump commands.

{% highlight bash %}
--compress, -C
{% endhighlight %}

Switch will tell mysql server to compress the dump on the fly so you can save a lot of bandwidth. However both sides needs to support the setting.
Note that you may also use that switch with mysql command.

## Dump consistency
It's also very important to not forget about doing the operation in one transaction. Otherwise (especially working on such a big data) you may end up with inconsistent dump.

{% highlight bash %}
--single-transaction
{% endhighlight %}


So in the end dump command might look like:
{% highlight bash %}
mysqldump -C --single-transaction database > database_dump.sql
{% endhighlight %}

