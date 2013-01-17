---
layout: post
title: Playing with Neo4J
tags:
- Beta
- Database
- Graphs
- Java
- JavaOne
- Neo4J
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Almost all of the apps I build rely heavily on <a href="http://en.wikipedia.org/wiki/Graph_theory">graphs</a> — not pretty charts, but rather networks of people, places, things, or concepts that relate to each other in different ways.  I've been looking for alternatives to standard table oriented relational databases, and the most interesting project I've found so far is <a href="http://neo4j.org/">Neo4J</a>.

The concept behind Neo4J is simple, and it's relatively easy to get started with if you're comfortable with Java.  The basic semantic concepts you work with are nodes, relationships, and properties.  For example, Peat (node) is friends (relationship) with Howard (node).  Nodes and relationships both support freeform key:value properties, so I could set a birthday on the Howard node, or a note about how we met on the Friend relationship.  Very simple and flexible.

The real power in Neo4J is in it's traversal system — complex graphs are pretty useless without being able to pull information out of them, and SQL based systems pretty much suck at handling complex queries through nested or recursive structures.  Neo4J's "traversers" are much simpler to build, and feel pretty darned quick.

What I'm really enjoying is the <em>simplicity</em> of the system.  The <a href="http://api.neo4j.org/current/">API</a> only describes 12 classes, and there's only 3 or 4 you need to be familiar with.  The jar file weighs in at under half a meg.  The "<a href="http://wiki.neo4j.org/content/One_Minute_Guide_Complete_Code">hello world</a>" example is readable straight out of the gate.  There's even a command line shell for exploring your data.  Simple concepts.  Easy to learn.  Small foot print.

Pretty cool stuff.

If your work involves designing and building systems that rely heavily on relationships, Neo4J is definitely worth checking out.  Caveats?  As of May 13th, it's still in beta — but it looks like the 1.0 release is around the corner.
