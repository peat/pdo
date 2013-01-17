---
layout: post
title: Watch Your Namespace
tags:
- Geek
status: publish
type: post
published: true
meta: {}
---
I helped a client troubleshoot a small "gotcha" in his Rails app this evening.  It's an odd problem he bumped into after refactoring a controller into a group of controllers -- a particularly spiffy feature of Rails.  For example, if you have a controller (say, <code>FooController</code>) that's getting rather large and unwieldy, you can break it up into smaller controllers in a <code>Foo</code> namespace:

<code>controllers/foo_controller.rb</code>

.. becomes ..

<code> controllers/foo/bar_controller.rb
controllers/foo/zed_controller.rb
controllers/foo/quux_controller.rb </code>

... and the controller class declaration changes from:

<code>class FooController &lt; ApplicationController</code>

... to ...

<code>class Foo::BarController &lt; ApplicationController</code>

... and so on for <code>Foo::ZedController</code> and <code>Foo::QuuxController</code>.  Pretty handy!  It should be noted that the controller routing changes as well, making <code>Foo::BarController#my_action</code> accessable as <code>http://mysite.com/foo/bar/my_action</code>.

<b>So here's the gotcha:</b>  if you're refactoring a <code>FooController</code>, chances are that you also have a <code>Foo</code> model (<code>models/foo.rb</code>).  The <code>Foo</code> model is declared as <code>class Foo</code>, which means you're suddenly mucking about in its namespace when you declare a controller as <code>Foo::BarController</code>. You're in trouble town with generic routing errors when you attempt to load<code> http://mysite.com/foo/bar/my_action</code>, and the way out isn't immediately apparent if you're not specifically looking for such collisions.

<b>The solution</b> is to change either the controller or model namespace to something else.  Controllers are a bit more flexible than models when it comes to naming, so changing <code>Foo::BarController</code> to <code>Foo<b>s</b>::BarController</code> and renaming the directory to <code>controllers/<b>foos</b>/bar_controller.rb</code> fixes the problem -- if you don't mind pluralized names.
