---
layout: post
title: Drinking Concurrently - Part 1
tags:
status: publish
type: post
published: true
meta: {}
---
_Part 1, wherein we drink beer and come to grips with locks and queues._

"Concurrency is hard."

If you're a software developer, you've probably heard that phrase quite a bit over the last few years. It crops up in conversations about how many cores a computer has, debates about web serving frameworks, and about how _amazing_ functional programming is.

Concurrency is a pervasive topic, and often a discouraging one.

Saying "concurrency is hard" will often kill a conversation. It's a defeating statement, an assertion that will leave many developers with furrowed brows and a sense of inadequacy.

Concurrency shouldn't have a bad rap. Concurrency is not a magical topic reserved for the neck-bearded druids of computer science. It does not require esoteric languages, or even a particularly robust vocabulary.

I'm writing this series of posts to help people understand concurrency, and to introduce common and accessible models for gracefully managing concurrent situations.

I intend to be gentle in this series, so we'll consider a common scenario that most of us are intimately familiar with: a pub. To enhance the mood, I recommend enjoying a beer while you continue reading. I guarantee you won't need all of your neurons for this particular exercise, so you may as well enjoy yourself!

## The Pub

So -- you and I arrive at the pub. It's a crowded Friday night, and we have to wait a few minutes before two seats open up at the bar. We sit down, and an attentive bartender takes our orders. We make awkward small talk until our drinks arrive. We hoist our glasses, toast to concurrency, and take a drink.

Oof, where to start? We were neck deep in concurrency problems before we took our first sip. Without much difficulty, we negotiated our way through queues, spinlocks, mutability, mutexes, actors, and synchronization.

Quick, take another drink! Forget I said any of that. We're taking it easy, right?

The pub scenario is repeated every night by millions of people who haven't the faintest idea that they're doing Difficult Computer Science. What they _do_ have is a common understanding about how to interact with other people when resources are scarce.

In other words, they understand how to _share_.

Sharing is the heart of concurrency. It doesn't matter if you're talking about threads, processes, processors, servers, or anything else -- everything active in a system must contend with sharing access to resources. Fortunately for us, all of these problems transcend computers, and become much easier to understand when we think about them in terms of simple human interactions.

Hence, the pub analogy.

Let's back it up and start from the beginning.

## Finding a Seat

A pub is not a nice restaurant where you can place a reservation ahead of time, or where the host will call your name when your table is ready -- a pub is usually a place where you stand around and watch for the next available seat.

The practice of constantly looking for an available seat is known as a _spinlock_. With no _maitre d'_ to notify you that your seat is ready, you must do the work of checking for an open spot at the bar. You can't just check once -- you must check over and over again. It is the simplest mechanism for determining if something is available, and we do it naturally and reflexively as humans. 

We can describe the situation as follows; forgive the lingo, but it's important:

- The activity of regularly looking for an open stool is called _spinning_.
- Sitting on a stool indicates that it is busy, and shouldn't be used by anyone else. The indicator is called a _lock_, and we can say a stool that is in use is _locked_.

Hence, spinlock.

This is simple to deal with when you're the only one looking for a seat, but it gets difficult when there's an uncontrolled herd of people lunging for every seat that becomes available.

There are a few ways the situation can get out of hand.

The worst is if someone accidentally shoves another person out of their seat (that is, they didn't check the lock). Bad things happen, man. Cops get involved, people get kicked out, chairs get thrown. That is the worst case scenario, but for the time being, let's assume that everyone checks locks before they try to sit down.

Even if everyone obeys the locking rule, we have to contend with a mob of people fighting over every seat that opens up. This is problematic because we have no control over who gets seated when: seats might be left empty as customers try to negotiate who goes first, and wallflowers will never be seated because they aren't assertive enough.

How do we bring order to the chaos of a busy Friday evening? How do we ensure that everyone gets a fair shot at the bar?

In a slightly more civilized pub the customers will simply wait in line. When a new customer arrives, they join the end of the line. The person at the front of the line is the only one in the spinlock -- everyone else just whips out their phones to check Facebook or Yelp.

The waiting line is a _first in, first out queue_ (or FIFO queue). Tangentially, some privileged parts of the world actually use the word "queue" instead of "waiting line;" they also have a propensity towards the metric system. It's all very civilized, but that's a discussion for another time.

Queues and locks work together as the foundation of every coherent concurrent system -- whether it's requesting a web page from a busy server, accessing data on a hard drive, waiting for a green light at an intersection, or getting a beer at the local pub.

It's queues and locks all the way down, baby.

## Next Up: Ordering a Drink

Queues and locks are well and good ... but spinlocks are terribly inefficient, and they won't help you order a beer from a busy bartender. How could we manage queues and locks more efficiently? How should we talk with the bar tender?

Coming soon!
