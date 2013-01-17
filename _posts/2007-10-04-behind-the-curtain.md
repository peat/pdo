---
layout: post
title: Behind the Curtain
tags:
- Amazon
- Architecture
- Awesome
- Java
status: publish
type: post
published: true
meta: {}
---
Here's an interesting excerpt from Werner Vogels' <a href="http://www.allthingsdistributed.com/2007/10/amazons_dynamo.html">Dynamo paper</a> about some of the guts behind Amazon's e-commerce platform:
<blockquote>"For example a page request to one of the e-commerce sites typically requires the rendering engine to construct its response by sending requests to<strong> over 150 services</strong>. These services often have multiple dependencies, which frequently are other services, and as such it is not uncommon for the call graph of an application to have more than one level."</blockquote>
There's no doubt Amazon uses extensive caching to keep performance up, but 150+ service calls to render a page  is remarkable, regardless of how you cut it.  Even more impressive is how all of these services are built around the assumption that something, somewhere is failing:  disks are crashing, networks are flapping, and processes are dying.

Check out the paper for more details.

Update:  It looks like Ars Technica got interested and put together a little <a href="http://arstechnica.com/news.ars/post/20071004-amazon-reveals-its-distributed-storage-dynamo.html">write up on Dynamo</a>.
