---
layout: post
title: Amazon EC2 + Persistent Storage
tags:
- Amazon
- EC2
status: publish
type: post
published: true
meta: {}
---
I received a friendly e-mail this morning from Amazon, announcing persistent storage for EC2 instances.  From the looks of it, the storage behaves like NAS -- it exists independent of the instances you're using, and can be mounted whenever you like.  Not bad.  I'm interested to see what the IO performance is like.

Other features include:

* Snapshots, to back up the storage to S3.
* Multiple volumes per instance.
* Shows up as a block device on the instance, so any filesystem can be used.

Persistent storage is in limited private beta right now, but according to the announcement it should be publicly available "later this year."
