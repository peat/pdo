---
layout: post
title: Amazon Elastic Compute Cloud
tags:
- Geek
status: publish
type: post
published: true
meta: {}
---
What the heck is the <a href="http://www.amazon.com/b/ref=sc_fe_c_1_3435361_1/102-9479326-4892141?ie=UTF8&amp;node=201590011" target="_blank">Amazon Elastic Compute Cloud</a>?  Ad hoc virtualized servers!  Hooray!

<b>Deploys in minutes</b>.  Upload an "Amazon Machine Image" (basically a Linux file system tar ball, kernel and all), use a web service call to turn it on ... and you're rockin'.

<b>Reasonable hardware, hot bandwidth</b>.  From the beta description:  "<span class="small">Each instance predictably provides the equivalent of a system with a </span><span class="small">1.7Ghz Xeon CPU, 1.75GB of RAM, 160GB of local disk, and 250Mb/s of network bandwidth."</span>

<b>Fair pricing</b>. 10 cents per instance hour; 20 cents per gigabyte of data sent; 15 cents per gigabyte of storage.

What does that all mean?  Well, you're looking at well equipped web server using 20GB of storage and 50GB of transfer per month for $85.  More or less instantly available.  HOT DAMN.  That's something that makes me want to throw my arms in the air and do a lot of dancing.

<span class="small">This is one of the most interesting things I've seen this year -- something that could be quite disruptive in the hosting industry. </span>  I'm chomping at the bit to get my beta invite.

Now, the next big issues: load balancing and network topology.  It's Linux, so LVS would work alright.  Tunnelling can provide a private network.  Hmm.  Food for thought, anyway.

--

Updates:
<ul>
	<li>The fine folks at Amazon have confirmed that these are <a href="http://www.cl.cam.ac.uk/Research/SRG/netos/xen/" target="_blank">Xen</a> virtual machines.</li>
	<li><a href="http://www.overstimulate.com/" target="_blank">Jesse Andrews</a> has a <a href="http://overstimulate.com/articles/2006/08/24/amazon-does-it-again.html" target="_blank">quick tutorial</a> on how to get an AMI running, and has an example AMI <a href="http://domu-12-31-33-00-04-9c.usma1.compute.amazonaws.com/" target="_blank">running Rails</a>.</li>
</ul>
