---
layout: post
title: EC2's Biggest Problem, Solved
tags:
- Amazon
- Coding
- EC2
status: publish
type: post
published: true
meta: {}
---
Amazon announced <a href="http://developer.amazonwebservices.com/connect/entry.jspa?externalID=1346">Elastic IP Addresses</a> for their <a href="http://www.amazon.com/gp/browse.html?node=201590011">Elastic Cloud Computing</a> (EC2) service this morning, which removes one of the biggest hurdles for deploying web sites on the service.  Previously, customers had no control over the IP addresses assigned to their EC2 instances, a frustrating situation for anyone wanting to reliably point a domain into the cloud.

Elastic IP Addresses solve this issue in a rather elegant way, by assigning a static IP address to your EC2 account, and providing a mechanism for routing that address to any of your EC2 instances.  This system provides a reliable address for DNS, and enables failover and takeover features for applications with high availability requirements.

Kudos to Amazon!
