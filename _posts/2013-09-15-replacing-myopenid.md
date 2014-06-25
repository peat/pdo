---
layout: post
title: Replacing MyOpenID.com
tags:
status: publish
type: post
published: true
meta: {}
---

If you use [myOpenID](http://myopenid.com/) to use your personal domain as an [OpenID](http://openid.net/), you're probably aware that the service will be turned off on February 1st, 2014.

I'm happy to say that there is now modern alternative that's free, and a *significant* upgrade: [IndieAuth.com](https://indieauth.com/) now supports OpenID delegation.

Like OpenID, IndieAuth.com allows you to sign into websites using your domain name. Technically speaking, it's an implementation of the open [RelMeAuth](http://microformats.org/wiki/RelMeAuth) protocol -- and the server is also [open source](https://github.com/aaronpk/IndieAuth), so you can run your own copy if you like.

This latest update to IndieAuth brings all of the flexibility of RelMeAuth authentication to the OpenID world, so now you can use the dozens of [supported authentication systems](https://github.com/intridea/omniauth/wiki/List-of-Strategies) to power your OpenID.

Switching to IndieAuth only takes three steps and about five minutes!

### Add RelMeAuth Tags To Your Domain's Home Page

To add authentication via GitHub, Twitter, and SMS:

<script src="https://gist.github.com/peat/6576572.js"></script>

You'll want to change my URLs to yours, of course.

The important part of these links is the `rel="me"` attribute. This is what IndieAuth looks for when attempting to determine what authentication options to present.

You can show or hide these any way you like, so long as the tags are present in your HTML.

### Add OpenID Tags To Your Domain's Home Page

In your `<head>`, insert the standard OpenID delegation tags:

<script src="https://gist.github.com/peat/6576582.js"></script>

Note that the `openid.delegate` value is *your* OpenID, where the `openid.server` should remain pointed at IndieAuth.com.

Yes, this is basic delegation. Support for OpenID 2.0 and Yadis discovery may be added in the future.

### Use Your OpenID

When you login to your favorite site (say, [StackExchange](http://stackexchange.com/login)), you will be prompted by IndieAuth to scan your page. If you've set up your `rel="me"` tags correctly, you'll be presented with a list of authentication providers.

Authenticate with your provider of choice, and your OpenID transaction will be completed by IndieAuth!

### Voilà

Congratulations: you've successfully moved off of myOpenID.com -- and gained more control over your identity.

*Hat tip to [aaronpk](http://aaronparecki.com/) for leading the charge on IndieAuth.com, and for organizing the [IndieAuth / OpenID Hackathon](http://indiewebcamp.com/events/2013-09-15-pdx-indieauth-openid-hackathon).*