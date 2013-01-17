---
layout: post
title: RPX in Action
tags:
- HTML
- JanRain
- Javascript
- OpenID
- OpenID Foundation
- Rails
- RPX
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
<a href="http://rpxnow.com">RPX</a> is a service from <a href="http://janrain.com">JanRain</a> that makes it easy to accept <a href="http://openid.net/">OpenIDs</a> for your web app.

Why is RPX useful?  Aren't there a bunch of OpenID plugins out there for [favorite language] or [preferred web development framework]?

There are a lot of libraries and plugins for a lot of platforms, but most of them have three problems: complexity, incompatibility, and poor usability.
<h3>The Old Way</h3>
<strong>Complexity:</strong>  Most of the existing tools require you to build database tables and maintain extra libraries on your production systems.  I like to avoid tools and libraries that step on my schema and cause extra maintenance work, and I expect you do too.

<strong>Incompatibility:</strong>  Most current tools don't fully support OpenID 2.0, which is a deal buster when you're trying to build a site for anyone who wants to accept <a href="http://en.wikipedia.org/wiki/I-name">i-names</a> or directed identities.

<strong>Usability:</strong>  Existing plugins don't usually provide a user friendly interface for the vast majority of people on the web.  User experience matters, and it's nice to get a helping hand when it's available.

RPX solves these issues in one swoop — it's mercifully <strong>simple, feature rich, and user friendly</strong>.

Did I mention free?  That's nice, too.
<h3>Seeking Simplicity</h3>
Here's what it takes to get RPX running with your app:
<ul>
	<li>A free account on rpxnow.com (premium accounts are available if you need extra features).</li>
	<li>A dab of Javascript on your login page (provided by <a href="http://rpxnow.com/">rpxnow.com</a>, example below).</li>
	<li>A few lines of code on your server side application (example below).</li>
</ul>

It took me less than half an hour to get it running the first time.

<h3>Feature Rich</h3>
Full support for OpenID 2.0 is a great thing — and not having to worry about future OpenID enhancements is even better.  But wait, there's more:  RPX provides authentication statistics, a testing tool, and a well documented API.  It also lets users authenticate with their Facebook and MySpace profiles.  It's the gift that keeps on giving.
<h3>User Friendly</h3>
RPX provides your visitors with a an attractive dialog that ushers them through the OpenID authentication process.  Even if they don't know what OpenID is, there are big friendly buttons that will help them use their accounts at Yahoo, AOL, Google, Facebook, or MySpace.  As more providers come online, RPX will update that interface on your behalf.

<h3>How Does It Work?</h3>
In a nutshell, RPX is a hosted service that handles the nitty gritty of the OpenID authentication process for you.  The only work for you is fetching the authentication information from the RPX server.

The flow looks something like this:
<ul>
	<li>I come to your web app and click the link to login.</li>
	<li>The RPX interface pops up and prompts me for my OpenID.</li>
	<li>After I authenticate with my OpenID provider, the RPX server directs me back to your app with a unique token.</li>
	<li>Your app queries the RPX server with that token, and gets my authentication information in return.</li>
</ul>
Pretty straight forward.  What's that look like in code?

A specific example (with <a href="http://rubyonrails.com/">Rails</a>) looks something like this:

<strong>The view (HTML + JS):</strong>

<pre><code>
&lt;a class="rpxnow" onclick="return false;" href="https://your-com.rpxnow.com/openid/v2/signin?token_url=http://your.com/rpx"&gt;Sign In&lt;/a&gt;

&lt;script src="https://rpxnow.com/openid/v2/widget" type="text/javascript"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
  RPXNOW.token_url = 'http://your.com/rpx';
  RPXNOW.realm = "mysite.com";
  RPXNOW.overlay = true;
&lt;/script&gt;
</code></pre>

The <code>token_url</code> in the link and the javascript points to a URL on your site, and the <code>RPXNOW.realm</code> is your OpenID authentication realm (typically the root URL for your site).

<strong>Rails handler at http://your.com/rpx:</strong>

<pre><code>
rpx_token = params[:token]

rpx = Net::HTTP.new('rpxnow.com', 443)
rpx.use_ssl = true
path = "/api/v2/auth_info"
args = "apiKey=#{RPX_API_KEY}&token=#{rpx_token}"
http_resp, response_data = rpx.post( path, args )

rpx_data = JSON.parse( response_data )
</code></pre>

Briefly stated, this code:
<ul>
	<li>Collects the token parameter from the user's request after they authenticate.</li>
	<li>Performs an HTTPS POST against the RPX server containing that token and a secret API key.</li>
	<li>Parses the JSON response into a usable format -- in this case, a hash named <code>rpx_data</code>.</li>
</ul>
This isn't limited to Rails, of course.  Every major development language and web framework can set up an HTTPS connection and parse JSON ... and if JSON isn't your style, you can get an XML response instead.
<h3>Real World Use</h3>
This morning I converted the <a href="http://openid.net/">OpenID Foundation's</a> <a href="https://openid.net/foundation/members/">membership website</a> to use RPX, and ditched the old plugin I hacked up to support the OpenID 2.0 features.  If you're interested in seeing it in action head on over to their site:  <a href="https://openid.net/foundation/members ">https://openid.net/foundation/members</a>

I also encourage anyone who's interested in the future of OpenID to become a member.  Individual memberships are cheap, and the pay off is big -- you can participate directly in the election of board members, review and ratify specifications, and participate in working groups.
<h3>Feedback</h3>
Still confused?  Know of a better solution?  Leave a comment, let me know!
