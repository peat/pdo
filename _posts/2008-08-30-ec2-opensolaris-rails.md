---
layout: post
title: EC2 + OpenSolaris + Rails
tags:
- Amazon
- EC2
- OpenSolaris
- Rails
- Ruby
- Sun
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
For the last couple of months I've spent a little time each week with the <a href="http://opensolaris.org/">OpenSolaris</a> team at <a href="http://sun.com/">Sun</a>, putting together an <a href="http://aws.amazon.com/ec2">Amazon EC2</a> image that makes it easy to deploy and experiment with <a href="http://rubyonrails.com/">Ruby on Rails</a>.

They released the AMI last Friday, but I've been too crazy busy to make an announcement.  <a href="http://developer.amazonwebservices.com/connect/entry.jspa?externalID=1438">Here's the official word</a>, and here's my take on it ...

My goal with this project was to help people get a Rails app running as quickly as possible.  We set up this AMI so that you can get your hands dirty with Rails if you don't want to spend the time installing everything on your home system or server, and it's an inexpensive and easy introduction to OpenSolaris if you're curious.

All the requisite goodies are pre-installed:  Rails 2.1, Mongrel, PostgreSQL and MySQL, Subversion, Git, Capistrano, and a few others choice gems.  You also get DTrace built into Ruby, if you're keen on that sort of thing.

There's also a sample Rails app in your home directory, and a pre-configured SMF file that serves as a handy introduction to the very handy <a href="http://www.sun.com/bigadmin/content/selfheal/smf-quickstart.jsp">Service Management Framework</a> -- the OpenSolaris system for managing daemons and other server processes.

Working with the OpenSolaris AMI team was a lot of fun, and in particular I'd like to give a thanks to <a href="http://blogs.sun.com/prashant/">Prashant</a> who did most of the hard work getting everything set up.
