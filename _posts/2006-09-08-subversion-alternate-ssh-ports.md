---
layout: post
title: Subversion + Alternate SSH Ports
tags:
- Geek
status: publish
type: post
published: true
meta: {}
---
One of my clients has a firewall in front of his subversion server, which is accessed within the network with the <code>svn+ssh</code> method. However, outside of the network it's a different story:  the tunnel through the firewall puts the public SSH interface on a non-standard port ... and <code>svn+ssh</code> doesn't play well with non-standard ports.

What's the work around?  A one line tweak in your personal Subversion configuration file.  I can only vouch for this on OS X, so your mileage may vary.
<ol>
	<li>Load <code>~/.subversion/config</code> into your favorite text editor.</li>
	<li>Add one line to the <code>[tunnels]</code> section:    <code>altssh = /usr/bin/ssh -p <i>alt_port</i></code></li>
</ol>
Then your access method to <code>svn+altssh</code> and you're ready to rock:

<code>svn checkout svn+altssh://me@host.com/path/to/repo</code>

This raises an interesting question:  what other non-standard methods are people using to access their repositories?

--

Update:  <a href="http://bendiken.net/" target="_blank">Arlo Bendiken</a> has a better solution to this particular problem in his comment below ... put the alternate port into the SSH config, so that any SSH interaction with the host receives the correct settings.  Thanks!
