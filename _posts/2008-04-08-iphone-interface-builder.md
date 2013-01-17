---
layout: post
title: iPhone + Interface Builder
tags:
- Apple
- Coding
- Interface Builder
- iPhone
- iPod Touch
- Objective C
- Programming
- SDK
status: publish
type: post
published: true
meta:
  _edit_last: '247897'
---
<em>Note: This is a little out of date, since the Beta 3 build automatically generates an empty XIB and the code for including it in new projects.  If you're looking for Apple's introductory tutorial on how to build applications with Interface Builder, <a href="http://developer.apple.com/iphone/library/documentation/iPhone/Conceptual/iPhone101/Articles/chapter_2_section_1.html">click here.</a></em>

So, the trick to using Interface Builder is figuring out where to put the files, and plugging the XIB interface into the app.

The file question is easily answered:  <em>File &gt; Write Class Files</em> to the directory in your project where the rest of your classes live.  For really simple apps with a single view, select your existing AppDelegate class and IB will merge the changes for you.  You'll also see a new .xib file in your classes directory, containing your interface.

Connecting the XIB interface is also relatively straight forward.  In your AppDelegate file, change what <code>self.contentView</code> points at:

<code>self.contentView = [[[NSBundle mainBundle] loadNibNamed:@"XIBFileName" owner:self <br/>options:nil] objectAtIndex:0];</code>

Where <code>XIBFileName</code> is the name of the generated XIB file without the .xib extension.

Anyhow.  I'm still learning, and this is with a beta release of the iPhone SDK, so you're welcome to leave comments if you have better ideas or tips on working with IB for the iPhone.  Thanks!
