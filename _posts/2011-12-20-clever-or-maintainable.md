---
layout: post
title: Is Your Code Clever or Maintainable?
tags:
- Bad Code
- Complexity
- Maintainability
- Ruby
- Software Development
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
<p>A few months ago, I found the following line of code in a CSS file:</p>

<pre style="overflow:auto; border: 1px solid #ddd; padding: 1em;">
div.updated { &lt;%= 'color: #800;' if DB.execute("SELECT id FROM sessions WHERE session_key=? LIMIT 1", params[:session_key]) %&gt; }
</pre>

<p>I expect most web developers with Ruby experience will be able to understand the code, and other developers should be able to sort it out without too much trouble.</p>

<p>That said:</p>

<ul>
<li>Did you have to read that line of code more than once?</li>
<li>Did you have a moment of distraction (e.g.: closing your eyes, looking out a window)?</li>
<li>Did you glaze over everything after the <code>if DB.execute</code> bit?</li>
</ul>

<p>I'll bet that all of you did at least one of those things, possibly all of those things, the <em>first time</em> you read this post. I know I had at least one mental hiccup when I discovered that little gem (and some architectural rage, but that's a post for another time).</p>

<p>Our working memories have a fairly well defined boundaries: We can track three seconds worth of data, or seven similar elements (depending on who you talk to). We have trouble maintaining integrity in our working memory when we switch between topics. We also have a subconscious reflex to distract ourselves (that is, a <em>preemptive</em> context switch) when faced with complexity that overloads our working memory.</p>

<p>These are basic human limitations. Some of us may have extraordinary talents that push these boundaries, but even so, the simplest software is complex enough to overwhelm our basic mental processes. </p>

<p>Fortunately, we humans are exceedingly good at building abstract mental models to represent complex concepts and patterns. One measure of software maintainability is how easy it is for other developers to learn and reconstruct those underlaying abstractions. In other words, how easy will it be to figure out what your code does?</p>

<p>Given our universal constraints, and the goal of making code easy to digest, lets look at that snippet again and see what we can do about it.</p>

<pre style="overflow:auto; border: 1px solid #ddd; padding: 1em;">
div.updated { &lt;%= 'color: #800;' if DB.execute("SELECT id FROM sessions WHERE session_key=? LIMIT 1", params[:session_key]) %&gt; }
</pre>

<p>The purpose of this code is both plausible and easy to comprehend: updated content on a web page is colored red when someone has an active session. Unfortunately, a developer seeing this code for the first time needs to understand 15 different concepts in 5 contexts on 1 line of code:</p>

<ul>
<li>The general CSS structure of the web site: we're working with the <code>updated</code> class of the <code>div</code> tag.</li>
<li>The template environment: we're working in <em>ERB</em> and <em>inserting</em> the result of a statement into the document.</li>
<li>The Ruby language and application server environment: the behavior of the <code>if</code> conditional, the scope of the <code>DB.execute</code> object and method, and the <code>params</code> object and <code>:session_key</code> symbol.</li>
<li>The database connector's binding style: the <em>replacement</em> of the <code>?</code> placeholder, and the <em>result</em> of the query.</li>
<li>The SQL and database structure: the relevence of the <code>id</code> and <code>session_key</code> columns in the <code>sessions</code> table.</li>
</ul>

<p>Ouch. There are clearly <em>too many</em> interdependent pieces to fit in your head in one shot &mdash; however, all of the dependencies must be satisfied for the code to work, so we don't have an opportunity to remove anything.</p>

<p>The first step towards easier comprehension is to break out of a single line of code. For better or worse, most of us think of a line of code as a discrete concept &mdash; like a sentence, or a simple action. </p>

<p>Even if we don't change the content of the code, we can make it considerably more readable by breaking it out into a few lines:</p>

<pre style="overflow:auto; border: 1px solid #ddd; padding: 1em;">
&lt;% if DB.execute("SELECT id FROM sessions WHERE session_key=? LIMIT 1", params[:session_key]) %&gt;
  div.updated { color: #800; }
&lt;% end %&gt;
</pre>

<p>Although the quantity of code has increased, it has been significantly simplified on a line-by-line basis, reducing our contextual overhead:</p>

<ul>
<li>The first line is still cumbersome, but at least it is limited to a single conditional statement containing Ruby, ERB, and SQL. As a conditional statement, it creates a simple context: we know we have an active session if we're inside of the block.</li>
<li>The second line is just CSS.</li>
<li>The third line closes the conditional block.</li>
</ul>

<p>That first line is still a bit problematic, though. What if we did something like this?</p>

<pre style="overflow:auto; border: 1px solid #ddd; padding: 1em;">
/* CSS File */
&lt;% if active_session_id() %&gt;
  div.updated { color: #800; }
&lt;% end %&gt;
</pre>

<pre style="overflow:auto; border: 1px solid #ddd; padding: 1em;">
# Ruby file
def active_session_id()
  DB.execute("SELECT id FROM sessions WHERE session_key=? LIMIT 1", params[:session_key])
end
</pre>

<p>We're still adding code, but we're also adding clarity:</p>

<ul>
<li>We've separated our primary concerns into independent pieces of code: first, determining when to change the style; second, how to detect whether we have an active session.</li>
<li>In the first part, we have a simple conditional statement, followed by the simple CSS, then the block closure. We are still exposed to the conditional statement in Ruby, but shielded from the mechanics of how the decision is made.</li>
<li>In the second part, we've define a method that checks the database. The context is our Ruby environment: even if it's a stand-alone Ruby file, we are free and clear of any concern about ERB, HTML, or CSS. It's also possible to reuse this code in other places.</li>
</ul>

<p>We're at a pretty good spot: a first encounter with this code is less likely to cause those mental hiccups we hit the first time around. Is there a better way to accomplish the same task? Is this a fairly trivial example? Undoubtedly yes, and well worth discussing some other time.</p>

<p>So, how did we get to that single line of code in the first place?</p>

<p>Lets revisit, for the fun of it:</p>

<pre style="overflow:auto; border: 1px solid #ddd; padding: 1em;">
div.updated { &lt;%= 'color: #800;' if DB.execute("SELECT id FROM sessions WHERE session_key=? LIMIT 1", params[:session_key]) %&gt; }
</pre>

<p>I bet you were able to read that in a single pass, right? No distraction, you just powered through it &mdash; because you already understand it. We've worked through the code in three different forms, and now we "get it." I'll bet a few of you have an inclination to see if you can tighten it up a little ... and therein lays the problem.</p>

<p>We rightly value concise answers, and find a lot of pleasure in simplifying complex systems. Unfortunately, we have a difficult time distinguishing between brevity and clarity when we're already intimately familiar with a section of code.</p>

<p>How do we determine if source code is clear, when we are thoroughly acquainted with it?</p>

<p>Here's a stab at figuring it out, from an objective perspective ...</p>

<p>For each line of code, score a point for each:</p>

<ul>
<li>Language you use</li>
<li>Conditional statement you introduce</li>
<li>Data structure you are dependent on, or change </li>
<li>Change of scope</li>
</ul>

<p>If have more than three or four points for a line of code, consider breaking it up into multiple lines, or refactoring the task into smaller pieces. </p>

<p>This clearly isn't something that you can do for every line of code, but a little practice can help you develop a healthy reflex for judging whether your code is "cleverly complex" or actually maintainable.</p>

<p>I'm thinking about writing more on maintainable software, addressing topics like languages, documentation, and releases. I'd love to hear what's most interesting to you. Leave a comment and tell me what you think!</p>
