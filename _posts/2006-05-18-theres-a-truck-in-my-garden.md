---
layout: post
title: There's a Truck in my Garden
tags:
- CSS
- Design
- HTML
status: publish
type: post
published: true
meta: {}
---
Last night I attended a great presentation by <a href="http://www.popart.com/">Pop Art</a> at the <a href="http://www.devgroupnw.com/">DevGroup NW</a> monthly meeting.  They have a very challenging project—building 30 custom sites in 30 weeks for <a href="http://www.selectrucks.com/">SelecTrucks</a>, the used truck arm of <a href="http://www.freightliner.com/">Freightliner</a>.

They patterned their approach around the <a href="http://www.csszengarden.com/">CSS Zen Garden</a> concept:
<ul>
	<li>Build a common XHTML template that gets syndicated to all of the different dealer sites.  No tables in the markup!</li>
	<li>Provide a completely customized design for each site, based entirely on CSS.</li>
</ul>
Here’s a couple examples that demonstrate how flexible this can be:
<ul>
	<li><a href="http://www.memphisselectrucks.com/">SelecTruck of Memphis</a></li>
	<li><a href="http://www.selectrucksmass.com/">SelecTruck of Massachussets</a></li>
	<li><a href="http://www.chicagoselectrucks.com/">SelecTruck of Chicago</a></li>
	<li><a href="http://louisvilleselectrucks.com/">SelecTruck of Louisville</a></li>
</ul>
Pretty darned <strong>wow</strong>.

Justin Garrity, Kelly White, Ryan Parr, and Dave Selden of Pop Art were on hand to talk about how the sites came together. Although Ben Fogarty wasn’t present, his designs certainly were.

Here’s a brief summary of the highlights ..
<h3>Design</h3>
Because of the extremely tight deadlines, the designers could only spend about 25 hours per site. They had to drop all of their heavy processes for sussing information out of clients, and instead depended entirely on an initial interview and a “half way” comp.

The initial interview had a process that really impressed me. They called it “word verses word.” Basically speaking, it was presenting the client with two contrasting words and having them pick one:
<ul>
	<li><strong>Modern</strong> v. <strong>Traditional</strong></li>
	<li><strong>Bold</strong> v. <strong>Classic</strong></li>
	<li><strong>Block</strong> v. <strong>Curvy</strong></li>
</ul>
You get the idea.  This is something I’ll definitely be incorporating into my client discussions in the future.
<h3>Tech</h3>
The sites are all served from a <a href="http://www.dotnetnuke.com/">DotNetNuke</a> backend.  The front end templating system was modified to produce clean XHTML templates, and they use browser sniffing to send stylesheets tailored specifically to the major platforms (IE 5.5/6, FireFox/Mozilla, Safari).

All of the graphics are alpha PNGs, and the designs make heavy use of layering to achieve the desired effects. They saved a huge amount of work by using CSS based layouts with “unsliced” graphics instead of tables and cut up image nightmares.

Much of the typography is done through the <a href="http://www.mikeindustries.com/sifr/">Scalable Inman Flash Replacement</a>, or <strong>sIFR</strong>.  sIFR replaces custom graphics as a way to display fonts outside the standard (and rather boring) core of web friendly fonts.

The mechanism is quite interesting: it examines an element in a page, loads a Flash file and scales it to fit inside of that element, and then inserts and scales the original text inside the element to fit the new Flash area. Simply put, you can maintain clean XHTML markup and a single Flash template, and sIFR does the rest.

Pretty darned awesome.

Pop Art has done an incredible job with such a complex project. They have some amazingly talented people on staff, and a good set of tools. Kudos!

As a side note, my cousin works at Freightliner and was able to give me a tour of the manufacturing floor at their Portland facility. It’s straight-up amazing to see these 100% custom trucks get assembled, painted, and accessorized ..

<strong>Update</strong>:  Ryan's posted a link to PopArt's official page for the <a href="http://www.popart.com/selectrucks/Default.aspx" target="_blank">SelecTrucks project</a>.
