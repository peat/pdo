---
layout: post
title: Saving More Money With S3?
tags:
- Amazon
- JanRain
- S3
- SmugMug
status: publish
type: post
published: true
meta: {}
---
I had lunch yesterday with some of the fine folks at <a href="http://janrain.com/">JanRain</a>, and one of our discussions was about <a href="http://www.amazon.com/gp/browse.html?node=16427261">Amazon's S3</a> ... can a business actually save money, using it for file storage and distribution?  It turns out there's a few pretty good cases for it, the most impressive being <a href="http://smugmug.com/">SmugMug</a> <a href="http://blogs.smugmug.com/don/2006/11/10/amazon-s3-show-me-the-money/">saving half a million bucks</a> vs. their DIY approach.

But things are changing in June.  <a href="http://www.amazon.com/gp/browse.html?node=16427261#price">Amazon unveiled a new pricing model for S3</a>, which is a little more complex than the previous $0.15 per gigabyte stored per month, with $0.20 per gigabyte transferred (simple, 'eh?).

The storage cost is the same, but transfers have been lowered and put into a tiered structure, and there's an additional charge for each request:
<ul>
	<li>$0.10 per GB - all data uploaded</li>
	<li>$0.18 per GB - first 10 TB / month data downloaded</li>
	<li>$0.16 per GB - next 40 TB / month data downloaded</li>
	<li>$0.13 per GB - data downloaded / month over 50 TB</li>
	<li>$0.01 per 1,000 PUT or LIST requests</li>
	<li>$0.01 per 10,000 GET and all other requests</li>
</ul>
I'm not a big fan of complexity, but Amazon seems to think it'll save most of us some money:
<blockquote><span class="small">"</span>If this new pricing had been applied to customers' March 2007 usage, 75% of customers would have seen their bill decrease, while an additional 11% would have seen an increase of less than 10%. Only 14% of customers would have experienced an increase of greater than 10%.<span class="small">"</span></blockquote>
Fair enough, I suppose.
