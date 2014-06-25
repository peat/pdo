---
layout: post
title: Take a Chance on an Intern
tags:
status: publish
type: post
published: true
meta: {}
---

Internships are about bootstrapping someone's career, a process plagued by naiveté and fraught with errors. Taking responsibility for a complete n00b is a vaguely horrifying prospect, particularly in the impatient and highly competitive culture of the software industry.

... But it's worth it.

I was 18 when I started a summer internship at the [Oregon Graduate Institute](http://en.wikipedia.org/wiki/OGI_School_of_Science_and_Engineering), and I was terrified.

I was the youngest person in the Data Intensive Systems Center, and I was way out of my league. I remember our regular update meetings, and being endlessly confounded by the pointed questions and topics at hand. 

Although I knew some C and had been teaching myself a bit about operating systems in my spare time, my first task was a real horror show: porting HPUX spinlocks to the Linux kernel.

It was my first experience drinking from the firehose. 

![Drink from the firehose](/images/drink-from-the-firehose.jpg)

I failed, miserably. It was rough. It took me a week to start comprehending the mechanics of the problem, much less grok the bigger concepts of concurrency and reentrant kernels. I got nowhere, and admitting defeat was awful.

Never the less, my boss continued to feed me projects and invited me to all of the meetings until we settled on something I was reasonably good at: breaking into servers. We focused on a systematic way to [prevent buffer overflow attacks](http://en.wikipedia.org/wiki/Buffer_overflow_protection), and the result was [a paper that had my name on it](https://www.usenix.org/legacy/publications/library/proceedings/sec98/cowan.html) -- one of ten authors.

The long term value of that experience was wildly lopsided in my favor. I was paid to learn about advanced security and computer science concepts, hack on the emerging Linux kernel, and work with brilliant people.

Although my contribution was mostly just testing and bechmarks, the experience was critical to building my career in tech.

What about the cost to OGI? Financially, it was three months of a low hourly wage. Otherwise, it was having the occasional conversation with an occasionally frustrated kid, and having the compassion to make room for an intern.

It's that last point that made the difference.

Hiring an intern is an exercise in compassion. It's giving someone opportunities to succeed, and helping them work through a significant amount of failure. It probably took me *much* longer than expected to complete simple tasks. I'm sure I sucked at asking for what I needed, because I didn't even know *what* I needed.

Compassion is not micromanagement. My boss's life would have been miserable if he checked in every couple of hours to correct my work before I had a chance to really think through my problems -- it would have sucked up all of his time, and I'd have been frustrated too.

In a similar vein, compassion is not coddling. An internship is work, not babysitting. I found a huge well of motivation because I was expected to contribute to *real* projects -- the more important the project, the better. I also learned that even the most critical projects had room for a neophyte like myself to get involved in testing, documentation, and supporting tools.

So I ran the gauntlet. By the end of three months, I was actually keeping up. My parting project that summer was an early prototype of a filesystem security module, which eventually evolved into [AppArmor](http://en.wikipedia.org/wiki/AppArmor) -- and is running on almost every Linux server in the world (I desperately hope none of my horrifying code survived that process).

In any case, I've been thinking a lot about internships now that I'm the one helping young developers get their foot in the door. I have been feeling particularly inspired and humbled by an award given to the authors of that paper I contributed to, 16 years ago:

![USENIX Security Test of Time 2013](/images/usenix-test-of-time.jpg)

My role was minor, but our team's achievement was significant. I am incredibly grateful to my boss, friends, and colleagues from OGI for taking a chance on an intern.

Portland has a wonderful and growing community of software developers, and I'll work to continue the trend of internships and mentoring in the years to come. I know there are other developers working on awesome projects who feel the same way.

Take a chance on an intern. It's worth it.
