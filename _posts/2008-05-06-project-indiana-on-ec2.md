---
layout: post
title: Project Indiana on EC2
tags:
- Amazon
- EC2
- OpenSolaris
- Project Indiana
- Sun
status: publish
type: post
published: true
meta:
  _searchme: '1'
  _edit_last: '247897'
---
<img src="http://www.opensolaris.com/images/opensolaris_logo_trans.png" style="float:right;padding-left:10px;" /> Interesting news this week -- along with the release of <a href="http://www.opensolaris.com/">Project Indiana</a>, Sun is also providing limited access to OpenSolaris images running on <a href="http://aws.amazon.com/ec2">Amazon's Elastic Compute Cloud</a>.  I'm keen to try it out, but at the same time I'm a little skeptical about the whole thing.

I have high hopes for Project Indiana.  After working with <a href="http://www.joyent.com/accelerator">Joyent Accelerators</a>, there are a lot of things I like about Solaris (the service manager, ZFS, DTrace, etc.) and a lot of things I don't like (awkward package management, very DIY for relatively simple things).

Indiana running on EC2 instances is a good way to introduce people to the platform, but it's a bummer you have to <a href="http://www.sun.com/third-party/global/amazon/index.jsp">register with Sun</a> and get their permission before jumping in the pool.  I hope the waiting list isn't too long.  I'm itching to play.

<img src="http://g-ecx.images-amazon.com/images/G/01/00/10/00/14/19/27/100014192753._V46777512_.gif" style="float:left;padding-right:10px;" />Hopefully Indiana on EC2 is lean, mean, and easy to get started with ... but I have my doubts that it will be a replacement for my current <a href="http://www.ubuntu.com/">Ubuntu</a> AMIs.  I don't have any super custom configurations, I just don't think EC2 isn't the kind of environment where Solaris really shines &mdash; EC2 is lots of little servers, not a big box with a bunch of cores and spindles.  Regardless, I'm an optimist, and I look forward to being proven wrong.

I'm waiting on access to the Project Indiana AMIs.  I'll report back as soon as I get my feet wet.

<em>Update:</em> I've been accepted to the beta program, but I don't think I can do a test drive until this weekend.  More information then!
