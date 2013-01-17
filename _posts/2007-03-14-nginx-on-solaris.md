---
layout: post
title: nginx on Solaris
tags:
- Business
- Geek
status: publish
type: post
published: true
meta: {}
---
We're continuing our evaluation of TextDrive / <a href="http://joyent.com/accelerator/" target="_blank">Joyent Accelerators</a>, and things are going well.  Tech support is responsive to my odd requests, the forums are lively, and the system itself is quite speedy.

Tonight we're installing <a href="http://nginx.net/" target="_blank">nginx</a> as the load balancing proxy for our Rails applications.  It's been personally recommended to us several times, battle tested by a few independent folks who are into these sorts of things, and received a lot of good press in the Rails community -- and it's mysteriously Russian.  So, we're quite interested to take it for a spin on our Accelerator.

First, there isn't a <a href="http://blastwave.org" target="_blank">Blastwave</a> package for nginx, so we built from the tarball (which requires the PCRE sources).  It's a pretty simple, although it took some troubleshooting.  The snag was that the PCRE build used tools that weren't in my default <code>$PATH</code>, but were in <code>/usr/ccs/bin</code>.

So:
<code>
$ export PATH=$PATH:/usr/ccs/bin
</code>

... and then we're off to the races:
<code>
$ wget http://sysoev.ru/nginx/nginx-x.x.x.tar.gz
$ wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-x.x.tar.gz
$ gtar zxf nginx-x.x.x.tar.gz pcre-x.x.tar.gz
$ cd nginx-x.x.x
$ ./configure --prefix=/opt/nginx --with-pcre=../pcre-x.x
$ make
$ sudo make install
</code>

PS:  <a href="http://weblog.rubyonrails.org/2007/3/14/rails-1-2-3-compatible-with-ruby-1-8-6-and-other-fixes" target="_blank">Rails 1.2.3</a> was released today.  And, happy birthday, Mom!
