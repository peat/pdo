---
layout: post
title: OpenSolaris on Amazon EC2, Part II
tags:
- Amazon
- Beta
- EC2
- OpenSolaris
- Sun
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
A few days ago I wrote about my <a href="http://peat.org/2008/05/14/opensolaris-on-amazon-ec2-review/">initial impressions</a> of the <a href="http://www.sun.com/third-party/global/amazon/index.jsp">OpenSolaris on Amazon EC2 beta</a>.  It was a little frustrating, however, the people who are running the program at Sun got in touch with me, and we spent some time talking on Friday morning about the experience.

The upshot of the conversation is that I think they're headed in the right direction.  We worked through some of the IPS and documentation issues I was having, and chatted about what they're working on over the next few weeks.  Specifically, they're in the process of building and releasing a set of AMIs built on OpenSolaris that target specific application environments -- for example, <a href="https://glassfish.dev.java.net/">GlassFish</a> for the Java EE folks, or <a href="http://rubyonrails.com/">Ruby on Rails</a>.

The first AMI they provided (ami-0c41a465) is just a blank slate, a trimmed down <a href="http://opensolaris.com/">OpenSolaris 2008.05</a> installation.  Those who are interested in the Apache/MySQL/PHP stack can tinker away by installing the 'amp-dev' package.

I finished the call feeling good about where the project is headed, and impressed by the people I spoke with.  In fact, I've volunteered a little time to help put together the Rails AMI next week.  If anyone has any favorite gems or other Rails goodies they'd like to see installed, let me know!

For more announcements about the OpenSolaris on EC2 program, head over to their blog at <a href="http://blogs.sun.com/ec2">http://blogs.sun.com/ec2</a>.
