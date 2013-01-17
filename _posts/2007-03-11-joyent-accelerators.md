---
layout: post
title: Joyent Accelerators
tags:
- Business
- Geek
status: publish
type: post
published: true
meta: {}
---
<a href="http://www.flickr.com/photos/textdriveinc/392668869/" target="_blank"><img src="http://farm1.static.flickr.com/148/392668869_3dccda008d_m.jpg" align="right" border="0" height="180" hspace="10" vspace="10" width="240" /></a>We're test driving a <a href="http://joyent.com/accelerator/" target="_blank">Joyent Accelerator</a> to see if a small cluster of them could be a reasonable replacement for our current hosting infrastructure.  So far, so good -- very speedy, and it looks like it'll be easier to scale when we need more horsepower.  For those not familiar, Joyent's Accelerators are <a href="http://www.sun.com/software/solaris/ds/utilization.jsp" target="_blank">Solaris containers</a>, Sun's OS-level virtualization technology.

There are only two snags I've hit so far:

<strong>Clutter.</strong>  When you get an Accelerator it comes preloaded with webmin, apache, php, mysql, courier, and all sorts of other things that people might want.  However, we're just deploying Rails apps, so the cruft has to go.  We've spent a fair amount of time getting rid of the clutter ... it would be GREAT if we could simply buy a bare-bones Accelerator.

<strong>Compilation.</strong>  The Accelerators are well equipped with <a href="http://www.blastwave.org/" target="_blank">Blastwave</a> packages for GCC and related tools, but Ruby wants to use Sun's compilers for building native extensions -- pretty critical to things like <a href="http://mongrel.rubyforge.org/" target="_blank">Mongrel</a> or <a href="http://projects.jkraemer.net/acts_as_ferret/wiki" target="_blank">acts_as_ferret</a>.  There is a posted workaround <a href="http://forum.textdrive.com/viewtopic.php?id=12630" target="_blank">here</a>, but it could be a pain to diagnose if you're not familiar with how gems are built.

Otherwise, it's all rock and roll.  Kudos to Joyent for getting this service off the ground -- despite it's rough edges, it's a great service.
