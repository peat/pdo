---
layout: post
title: Eventual Consistency, Explained
tags:
- ACID
- Amazon
- Database
- Latency
- PHP
- Ruby on Rails
- SimpleDB
- Web Services
- Werner Vogels
status: publish
type: post
published: true
meta: {}
---
<a href="http://www.allthingsdistributed.com/">Werner Vogels</a>, the CTO at Amazon, has a <a href="http://www.allthingsdistributed.com/2007/12/eventually_consistent.html">great post</a> about the contentious idea of "eventual consistency" for the new <a href="http://www.amazon.com/gp/browse.html?node=342335011">SimpleDB</a> service.  The idea that a database could be inconsistent is a little disconcerting to a lot of people -- after all, inconsistent means unpredictable, and that just doesn't fly for us deterministic computer people.  Right?

Well, "eventual consistency" isn't entirely unpredictable.  And, it has it's benefits -- especially when it means avoiding locking on highly concurrent read and write operations.  That's exactly what SimpleDB was designed to do.  To quote Vogels:
<blockquote>"Inconsistency can be tolerated for two reasons: for improving read and write performance under highly concurrent conditions and for handling partition cases where a majority model would render part of the system unavailable even though the nodes are up and running.</blockquote>
<blockquote>"Whether or not inconsistencies are acceptable depends on the client application. A specific popular case is a website scenario in which we can have the notion of user-perceived consistency; the inconsistency window needs to be smaller than the time expected for the customer to return for the next page load. This allows for updates to propagate through the system, before the next read is expected."</blockquote>
<blockquote>(from "<a href="http://www.allthingsdistributed.com/2007/12/eventually_consistent.html">Eventually Consistent</a>")</blockquote>
<blockquote></blockquote>
SimpleDB was intentionally designed to behave this way, which means it certainly wasn't built to  replace traditional <a href="http://en.wikipedia.org/wiki/ACID">ACID</a> <a href="http://en.wikipedia.org/wiki/Relational_database">relational databases</a> for all scenarios.  If you think about how often you require <em>immediate</em> consistency in your web applications, you'll likely find that a very significant portion of your database interactions don't.

My biggest concern about SimpleDB isn't consistency or relationships, it's latency. SimpleDB queries from outside of the Amazon cloud won't be fast enough to feed sites that require more than a couple of queries per page -- unless those queries can be executed in parallel, which isn't an easy option in single-threaded web environments (PHP, Rails, etc.).

I'm excited to see how it operates with parallel queries, though.  If an application is built to make dozens of queries simultaneously, rather than sequentially, the performance could be excellent.

I have a little Java toolkit for querying web services in parallel, and I'm itching to unleash it on SimpleDB.  All this hot air blowing isn't worth much without real numbers, right? :)
