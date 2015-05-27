---
layout: post
title:  "Interesting sysdig Commands"
date:   2015-05-27 10:16:00
categories: linux systems monitoring performance debug
---
This is really just about some commands that I've found interesting with `sysdig`. As I find more I intend to update this post.

First some `sysdig` boilerplate:
{% highlight bash %}
# Capture events for later analysis
sysdig -w myfile.scap

# Read events from a capture file
sysdig -r myfile.scap

# List all available fields
sysdig -l

# List all chisels
sysdig -cl
{% endhighlight %}

Now for the commands:
{% highlight bash %}
# Lists all write to file events and their payload from processes named gcc-config (ignores un-named files like stdout)
sysdig -c echo_fds proc.name=gcc-config and evt.is_io_write=true and fd.name!=''

# Show the network data exchanged with a host
sysdig -s2000 -A -c echo_fds fd.cip=102.168.0.1

# List the processes with the most open files
sysdig -c fdcount_by proc.name "fd.type=file"
{% endhighlight %}

