---
layout: post
title: null Considered Harmful
tags:
status: publish
type: post
published: true
meta: {}
---

I've spent enough time ranting about `null` in the last few years that I feel like I need to explain myself, lest I begin to sound like an unhinged maniac.

In almost every software project I've been a part of, the majority of errors I've encountered are caused by unexpected null references. Many are caught at compile or test time, but they always creep though, and few platforms are exempt. They crop up everywhere: web applications, desktop applications, embedded software, game consoles, mobile devices -- almost everywhere there is software, there are null references.

What causes these bugs?

For the most part, it's because software developers don't check for null references before attempting to access a variable, and nulls happen more often than we expect: they might come from a database, or as the result of a missing data in an API call, or a race condition, or through innumerable other scenarios that developers _can't reasonably anticipate_.

Dealing with null references are part and parcel of being a software developer, because null reference is a _deliberate feature_ of most programming languages: it's a rather ambiguous concept used to indicate that a value is not available, or for reserving an "empty" variable to ensure structure or scope.

The problem with null is that if it's an option for _any_ variable, accidental null references are a concern for _every_ variable. There are obvious and trivial examples where it's not worth worrying about, but given the prevalence of unexpected null references, this is clearly a problem.

Lets take a brief detour to a similar kind of issue: memory management.

Software developers who work in languages with explicit memory management and addressing must be well disciplined, or their code will suffer from memory leaks, stray pointers, and other related issues.

This became a big enough problem that language designers decided that developers should be protected from the mechanics of memory management. While developers still need to worry about the efficient use of memory, they are shielded from explicit controls over how memory is allocated and addressed. Taking memory management away from developers eliminated an entire class of concerns.

What does this have to do with null references?

Software developers who work in languages with explicit null assignment and checking must be well disciplined, or their code will suffer from unexpected null references.

Null references have become a big enough problem that developers should be protected from the mechanics of null assignment and checking. While developers still need to worry about ambiguous data and scope placeholders, they should be shielded from explicit assignment and access to null values. Taking explicit null management away from developers will eliminate an entire class of concerns.

Sound familiar?

In other words, languages that support null references are going to be more prone to errors, and accumulate more technical debt -- just like languages that support explicit memory management will be more prone to errors, and accumulate more technical debt.

To paraphrase [Dijkstra](http://www.u.arizona.edu/~rubinson/copyright_violations/Go_To_Considered_Harmful.html), I have become convinced that null references should be abolished from all "higher level" programming languages.