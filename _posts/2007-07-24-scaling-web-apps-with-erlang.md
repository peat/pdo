---
layout: post
title: Scaling Web Apps With Erlang?
tags:
- Erlang
- Programming
status: publish
type: post
published: true
meta: {}
---
In my spare time I'm doing a little hacking with <a href="http://erlang.org/">Erlang</a>.  It's an interesting language.  I'm still warming up to  functional programming, but the rest of it makes a lot of sense:  immutable variables aren't as big a headache as I expected, the message passing is easy and cheap, and light weight threading without worries is a genuine pleasure.  Plus, the performance is excellent.

The reason for my interest is that in the next year or so, I have several projects that are going to bottleneck on the database.  Which got me thinking about caching, synchronization, and distributing data across multiple servers.  The popular solution is to use memcached, slice up the database, and write a custom layer for managing the cache and database.  It's a non-trivial task, and there are two problems that get solved over and over, both have to do with synchronization:
<ol>
	<li>Cache synchronization requirements are variable.  Some things needs to be updated in real time (like shopping carts), some can be loose by a few minutes (e-mail), and some can wait around for hours or days (aggregate statistics, relatively static content).</li>
	<li>Server-to-server synchronization of cached data is not variable. It doesn't have to be instant, but it needs to be predictable.</li>
</ol>
All of this has to happen while serving thousands of requests per second, and the whole ball of wax needs to have tight error and exception handling.  So, as a mere Erlang noob, the hype sounds like a good fit.  ;-)

Regardless -- I'm sure there are other people working to solve the caching problem, and I'd love to hear their thoughts.
