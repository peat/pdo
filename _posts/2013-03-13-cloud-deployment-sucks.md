---
layout: post
title: "Cloud Deployment Sucks"
tags:
status: draft
type: post
published: true
meta: {}
---
I've spent a month flagellating myself with cloud deployment and configuration management tools, and I'm not happy about it.

We work in a remarkable world where cheap laptops have gigs of memory and multiple cores, where virtual servers can be created and dismissed in seconds, and where production software environments evolve on a daily (if not hourly) basis. Even our coffee shops have multi-megabit Internet connections.

And yet ... **Cloud deployment sucks.**

### Fast and Ephemeral

Servers in the cloud are disposable. A new application server can be ready to go in about two minutes -- and I don't mean "two minutes to boot, then wait ten minutes to install the configuration management software environment and grind through instructions before it's ready to go."

I mean _ready to go_ in two minutes. Deployed. Added to the cluster, and taking traffic from the load balancer.

The most powerful aspect of the cloud is the speed of server deployment, and this capability is largely ignored by configuration management tools.

### All or Nothing

Given how easy it is to deploy a new server in the cloud, we shouldn't have to worry about fine grained state management for server configuration.

Why?

Which of these two scenarios sounds more appealing:

**Scenario A**: Writing configuration scripts in a vendor-specific DSL that _must_ be idempotent to successfully roll back and forth through configuration change requests, while tracking the runtime lifecycle of a multi-system configuration management tool so that you know when and where server specific data is available.

**Scenario B**: Writing shell scripts that take a machine from boot to deployment.

In a perfect world, where software is easy and I have lots of time to learn new things, Scenario A is very attractive. I'm a nerd. I like to learn lots and have fun.

In the real world, I have a limited amount of time to deal with failures while developing my configurations. In the case where something goes wrong (and it always will), I want to work in Scenario B.

Why?

In Scenario A, a system will be left in an unknown state unless it's dealing with the simplest of configurations. Rollbacks mutate the state of a system _after_ the point of failure, configuration management tools add another layer of complexity to debug, and many tools have configuration actions that can be triggered by outside events ... _even when the server is in a failed state_.

In Scenario B, a server is left in the state in which the configuration failed. Debugging is significantly easier in a static environment, with the added bonus of debugging in the same environment your scripts target -- a shell.

When I'm developing a configuration for a server, I want an "all or nothing" environment that lends itself to replicating and debugging failures as quickly as possible. **I want a server to fail fast and fail hard when something goes wrong**, and I want to use the same techniques and languages to develop the configuration as I use to debug a failure.

### What About The Hardware?

Another beautiful thing about deploying in the cloud is being able to configure hardware profiles to match the applications.

Running MongoDB? You want RAID 1+0 storage on 4+ volumes, with a spare drive for fail over. You also want a ton of memory, and a bunch of cores.

Running a Redis cache? Who cares about storage or CPU -- you want memory!

Running a Rails app? Bring on the CPU and RAM.

**Applications and hardware are intimately related**, and it should be easy to experiment with the configuration of your hardware as well as your software. The cloud makes it easy to deploy different kinds of servers running different kinds of applications -- why doesn't configuration management software take this to heart?

### The Oprah Moment 

_"You get a cluster! And you get a cluster! And you get a cluster! Everybody gets a cluster!"_

It's fast to start single machines -- why not make it fast to start up an entire cluster for each of your developers, or for a demo?

A configuration tool should make it drop dead simple to clone or scale independent clusters of servers. Migrating data is always a bear, but sharing configuration state between servers is not.

Which brings me to the next point.

### Server Central

Many configuration management tools _need_ a central control or search server.

Really? Why?

Central control servers and configuration management daemons are nearly useless in a cloud environment, once you take away the dependency on granular configuration management on long running systems. Extra daemons and servers increase the complexity of your deployments, and introduce more opportunities for attackers.

All modern cloud APIs have extensive support for describing and discovering systems. If they don't offer the specific information you need, consider the fact that a cheap laptop can run _hundreds_ of simultaneous SSH connections to remote systems.

Even without a central configuration management server, you can discover and distribute shared configuration data to dozens of servers in a matter of seconds. From a cheap laptop. In a coffee shop.

### Ragequit, Reboot

Last week I stormed out of the office after a month of getting bitten in the ass by exceedingly slow, fragile, and excruciatingly complex configuration management tools.

Almost everyone I've talked to about configuration management is pissed off by the compromises they have to make when working in the cloud.

Everything in this blog post is possible to achieve -- I know because I've written my own tools for doing _all of the above_ over the last couple of days.

That said, I'm not attracted to the idea of maintaining this code if there happens to be a configuration management tool that already fills the bill.

Is there one? What's your take?