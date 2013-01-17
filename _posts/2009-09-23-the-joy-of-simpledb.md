---
layout: post
title: The Joy of SimpleDB
tags:
- Amazon
- BrowserMob
- Cloud Computing
- Databases
- SimpleDB
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Amazon's <a href="http://aws.amazon.com/simpledb/">SimpleDB</a> is one of the hardest of their services to understand, despite being one of the simplest.  I think the difficult part is getting over the "database" in the description -- we're prone to start comparing it with the relational databases we work with every day, and unfortunately that's not a reasonable comparison.

Think of it this way:  SimpleDB is a big hash of hashes that's web accessible.  That's basically it.  You get to store arbitrary sets of key-value pairs, each with it's own unique identifier, in a big bucket in the sky.

Huh.  Interesting.  So where would you use SimpleDB instead of a traditional relational database?

There are two things that SimpleDB handles incredibly well: concurrency, and accessibility.

SimpleDB is designed to stay responsive to queries even when you're pumping it full of records.  Logging and analysis is a great example of this, and a great example is <a href="http://browsermob.com/">BrowserMob</a>'s monitoring service.  They poke your site every few minutes to ensure it's responding -- but it's not just checking to see that your web server is alive, but also monitoring the load time for every object in the page:  images, CSS files, etc.  You can check the status and compare responses over time to see how your site is doing as it gets more popular, and as you change pieces under the hood.  The data from all of the sites they monitor are pumped into SimpleDB, and the results are available for their customers to see in real time.<sup>1</sup>

That level of concurrency, of accepting a substantial number of simultaneous writes while querying the complete data set, is hard to do, especially when every piece of the data is being indexed.  Most relational databases fall over pretty quick, but SimpleDB keeps on ticking.

The second thing that SimpleDB excels at is being accessible.  It's available to any device that can talk to the web: your computer, of course, but also phones (even the cheap ones), game consoles (portables too), DVD players, information kiosks, environmental monitors, toasters, etc.  Instead of building a web service around a traditional database, you can save a lot of time, energy, and frustration by using SimpleDB as queryable, web accessible, data storage.<sup>2</sup>

... But only if your data model works with SimpleDB, of course.  There are some drawbacks, like eventual consistency, no transactions, and weak constraints that make it difficult or impossible to use for many applications.  Never the less, it's an important tool to have in your toolbox -- a complement rather than competition to traditional RDBMSes.

Last week I gave a presentation at "The Act of Making Clouds" on SimpleDB.  I touched on some of these subjects, and although there isn't an audio track, you're welcome to check out the deck, below.
<div id="__ss_2018872" style="width: 425px; text-align: left;"><object style="margin:0px" classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" width="425" height="355" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,40,0"><param name="allowFullScreen" value="true" /><param name="allowScriptAccess" value="always" /><param name="src" value="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=sao-simpledb-whywhathow-090918122550-phpapp01&amp;stripped_title=simpledb-why-what-and-how" /><param name="allowfullscreen" value="true" /><embed style="margin:0px" type="application/x-shockwave-flash" width="425" height="355" src="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=sao-simpledb-whywhathow-090918122550-phpapp01&amp;stripped_title=simpledb-why-what-and-how" allowscriptaccess="always" allowfullscreen="true"></embed></object></div>
<div style="color: #888">1. "real time" defined as within a few seconds; eventual consistency is exactly that.
2. Also check out <a href="http://couchdb.apache.org/">CouchDB</a>.  It's a web accessible hash of hashes that you can manage yourself!</div>
