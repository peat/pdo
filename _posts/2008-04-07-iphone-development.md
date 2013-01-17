---
layout: post
title: iPhone Development - First Impressions
tags:
- Apple
- Awesome
- Banknotes
- Coding
- iPhone
- iPod Touch
- Objective C
- Programming
- Web Services
status: publish
type: post
published: true
meta:
  _edit_last: '247897'
---
I spent the weekend building a native iPhone app.  It's unfinished, and a little rough around the edges ... but I'm happy with the experience so far.

The concept is relatively simple:  I want an app to search through (and show off) my collection of international banknotes when I'm out and about.

There are a few hurdles, though.

For example, it's been over a decade since I worked on a reasonably sized C application.  So, I'm getting back into the swing of things with Objective-C style pointers and memory management, and remembering how much I hate segmentation faults and bus errors.

Also, being new to Objective-C <em>and</em> Mac development, this learning curve looks a bit like a wall.  Thankfully, there is quite a bit of sample code out there, but it's not entirely consistent ... which I guess is par for the course for a beta development system and a OS that hasn't been released yet.

I'm learning, but I'm pretty sure my code is gnarly enough to make a Real Mac Developer nauseous.  That said, if you are a Real Mac Developer with a strong stomach, please drop me a line -- I'd love to show you what I have, just so that you can tell me how bad it really is (and, hopefully, tell me how I can make it better).

At this point in the game, there are a few things I'm very pleased with:
<ol>
	<li>Interacting with the Internet and web services is incredibly easy.  Support for synchronous and asynchronous HTTP requests and very flexible caching policies make for a happy web service developer. This is particularly nice since the guts of the database and searching features will be powered by a Rails app siting on a server somewhere else.</li>
	<li>Working with XML is also very pleasant.  NSXML can handle proper XPath and XQuery searches, which is really quite nice.  The documentation is very mature for this and the other supported NS* classes, and there are plenty of examples out there on the net.</li>
	<li>UIKit follows very sane MVC and delegation patterns.  It's pretty straight forward and consistent.</li>
</ol>
And, of course, a few things I'm rather surprised to find, and desperately hope for resolution on:
<ol>
	<li><strike>The iPhone simulator isn't entirely safe. My hamfisted techniques have somehow caused other apps (including Finder) to crash several times.  It's terribly frustrating, and makes me a bit nervous about experimenting.</strike> I'm not sure if I'm getting better, or if the recent betas have been more stable, but I haven't had any catastrophic errors recently.</li>
	<li>No (official) coverflow interface.  Wow.  This is perfectly suited for what I want to do, and a big part of what makes the iPhone such a compelling platform to develop for.  Please, please, please include this in the final release.</li>
	<li><strike>I see Interface Builder ... but absolutely no documentation on how to use it for an iPhone.  Can someone point me at an example?</strike>  Apple now has a <a href="http://developer.apple.com/iphone/library/documentation/iPhone/Conceptual/iPhone101/Articles/chapter_2_section_1.html">step-by-step guide</a> to building a simple app on the iPhone with Interface builder.  I also found an example <a href="http://techblog.muthuka.com/index.php/2008/03/27/hello-world-iphone-native-application/">here</a> and posted my own <a href="http://peat.wordpress.com/2008/04/08/iphone-interface-builder/">followup summary</a> for people who are already familiar with Interface Builder, and just want to see how to plug in their interfaces.</li>
</ol>
Anyhow, good points and bad points, but on the whole it's been a good experience so far.  The NS* classes are all stable and well documented, and the UI* classes and documentation are about what you'd expect from an API in beta.

I'm keen to get a code review from someone who knows what they're doing, and I'm eagerly awaiting the next update to see what's changed.  Unfortunately, I think I'll have to have to wait until June to get a real iPhone -- I'm betting that the next generation iPhone will be released along with the SDK and OS 2.0 at WWDC '08.

<strong>Update:</strong>  I found an <a href="http://techblog.muthuka.com/index.php/2008/03/27/hello-world-iphone-native-application/">Interface Builder + iPhone tutorial</a>, and I posted a <a href="http://peat.wordpress.com/2008/04/08/iphone-interface-builder/">short summary about how to interface with the IB files</a>.
