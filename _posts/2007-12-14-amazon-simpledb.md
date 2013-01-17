---
layout: post
title: Amazon SimpleDB
tags:
- Amazon
- SimpleDB
status: publish
type: post
published: true
meta: {}
---
Amazon will soon be releasing their <a href="http://www.amazon.com/b/ref=sc_fe_c_1_3435361_1?ie=UTF8&amp;node=342335011&amp;no=3435361&amp;me=A36L942TSJ2AJA">SimpleDB</a> service under a limited beta program.

I'm very excited about this.  Persistent, high performance databases are a big missing piece in Amazon's cloud computing initiative -- <a href="http://www.amazon.com/gp/browse.html?node=201590011">EC2</a> doesn't offer storage that persists across reboots, and <a href="http://www.amazon.com/gp/browse.html?node=16427261">S3</a> isn't structured to provide the IO required by a database.

Conceptually, SimpleDB is very compelling.  It's designed for real time querying, has no hard limits on storage, and is metered based on storage and CPU time.  It looks a lot like Amazon's <a href="http://www.allthingsdistributed.com/2007/10/amazons_dynamo.html">Dynamo</a> technology ... and it wouldn't surprise me if they released the Dynamo paper to gauge interest in exposing such a service.

But, there are three big caveats.<span class="Apple-style-span" style="font-weight:bold;"></span>

<span class="Apple-style-span" style="font-weight:bold;">It's not SQL</span>.  This isn't actually as big a deal as it seems, but I know there are going to be a lot of people who are bent out of shape on this one.  Why isn't it a big deal?  Because ... <span class="Apple-style-span" style="font-weight:bold;"></span><span class="Apple-style-span" style="font-weight:bold;"></span>

<span class="Apple-style-span" style="font-weight:bold;">It's not relational</span>.  SimpleDB provides a big flat table, with arbitrary attributes per row.  So, queries are all about filtering through data, and while they can have very complex rules, it doesn't behave like the "normal" relational databases we're accustomed to using.

<span class="Apple-style-span" style="font-weight:bold;"></span><span class="Apple-style-span" style="font-weight:bold;">Updates are "eventually consistent."</span>  This means that if you immediately query for data you just pushed into SimpleDB, it may not show up.  You have a guarantee that it will show up within a few seconds, but not immediately.  Amazon calls this "eventual consistency."

It may be a little scary for some folks who are most comfortable with the traditional model of building apps around a single relational database.  On the other hand, it appears to be a great system for people who have built big websites, and are already comfortable dealing with lazy synchronization and custom data sources.

I'm looking forward to playing with it!

(Tip o' the hat to @grigs)

Update:  <a href="http://www.satine.org/archives/2007/12/13/amazon-simpledb/">Here's a great post</a> that goes into a little more detail about the give and take of SimpleDB.  Fun fact:  it's written in Erlang.

Update:  More stats.  Looks like their opening offering lets you create up to 100 "domains" containing up to 10 GB of data each.   That's a good start.
