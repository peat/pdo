---
layout: post
title: Rails + Joyent Accelerator Benchmark
tags:
- Business
- Geek
status: publish
type: post
published: true
meta:
  _wp_old_slug: rails-nginx-joyent-accelerator-benchmark
---
Well, this is fun.   Here's the configuration:
<ul>
	<li><a href="http://joyent.com/accelerator" target="_blank">Joyent Accelerator 64-L</a> -- We stripped it down and built it back up with the bare minimum <a href="http://blastwave.org/" target="_blank">Blastwave</a> packages we need to run our apps (surprisingly few).</li>
	<li><a href="http://rubyonrails.org/" target="_blank">Rails</a> 1.2.2 Application  -- Moderate DB complexity, loaded with fixture data, and using <a href="http://projects.jkraemer.net/acts_as_ferret" target="_blank">acts_as_ferret</a> extensively.  No optimization at all (caching, query tweaking, etc.).</li>
	<li><a href="http://mongrel.rubyforge.org/" target="_blank">Mongrel</a> 1.0.1 -- Running in production mode as a cluster with 4 instances (I think the server has 4 processor cores).</li>
	<li><a href="http://nginx.net/" target="_blank">nginx</a> 0.5.14 -- <a href="http://peat.wordpress.com/2007/03/14/nginx-on-solaris/" target="_blank">Built from scratch</a>, and running the generic <a href="http://wiki.codemongers.com/NginxRubyonRailsMongrel" target="_blank">Rails/Mongrel configuration</a> found on the wiki.</li>
	<li><a href="http://postgresql.org/" target="_blank">PostgreSQL</a> 8.1.4 -- Out of the box configuration from the Blastwave package (nothing special, no ANALYZE statements).</li>
</ul>
We're seeing about 50 connections served per second, with 80% of pages delivered within 150ms, and zero dropped or failed connections.  I'm pretty sure we can double that if we spent any time optimizing the application and server stack.

Not bad .. but the big fat caveat is that it's 11:00 PM so our box obviously isn't loaded very heavily.  We can burst up to 95% CPU utilization on the machine, so of course these numbers don't reflect reality of peak hours.  That said, we've never seen load reported over 0.2, even during peak.

I'm happy!

Update:  I should note that the 50/sec rate is for a pretty dynamic application with some bells and whistles; connections for static content are in the hundreds per second, but not too applicable for our purposes.
