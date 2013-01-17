---
layout: post
title: Determining Technical Requirements
tags:
- Business
- Estimates
- Project Management
- Software
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
Estimates for software are terrible, terrible things.  When I was a budding web developer, I thought I had it pretty much figured out:  X hours to solve the stated problem, X hours to write the code and tests, then double the sum (aka, "the optimistic compensation adjustment").

That worked alright when my job was just writing code, but utterly failed when I struck out on my own.  Aside from figuring out how to budget for planning, communication, integration, and deployment ... I also realized that I brought a huge number of technical assumptions to the table, and that my assumptions weren't always in line with what the customer needed.

So, over the last several years I've compiled a set of questions that help me better understand the general technical requirements for a project.  It isn't comprehensive or complete -- you can't fill out the form, pull a lever, and have an estimate shoot out -- but it is a good starting point, and has helped me quickly figure out a the client's expectations and experience with building web applications.

Chances are you'll have to put on your expert hat and coach your clients through some of these questions (and their implications) ... but that's what they're paying you for, right?

So, without further ado ...
<h3>Accessibility</h3>
<ul>
	<li>What are the minimum requirements for devices and browsers we should support? <em>(eg: a modern computer running IE 6+, FF 2+, or Safari 2+)</em></li>
	<li>What accommodations are necessary for impaired individuals?  <em>(eg: adjustable font sizes for the visually impaired, tactile interfaces for the blind and deaf)</em></li>
	<li>Are there specific accessibility regulations that may apply to this project? <em>(eg: Section 508)</em></li>
</ul>
<h3>Reliability and Recovery</h3>
<ul>
	<li>What are the primary usage hours? <em>(eg: business hours across the continental United States)</em></li>
	<li>What is the maximum acceptable downtime during primary usage hours? <em>(eg: 4 hours down per month)</em></li>
	<li>What disaster scenarios should we have a contingency plan for?  <em>(eg: failed hard drive, hurricane, nuclear war)</em></li>
</ul>
<h3>Performance and Scaling</h3>
<ul>
	<li>Approximately how many people are expected to interact with the system during peak hours?</li>
	<li>Approximately how much tabular data will the system be managing?  <em>(eg: contact information, dates, product descriptions, etc.)</em></li>
	<li>Approximately how much binary data will the system be managing?  <em>(eg: photographs, music, video, etc.)</em></li>
	<li>How many reports need to be available in real time, and how many can be run in periodic batches?</li>
	<li>What is the minimum acceptable load time for interactive pages? <em>(eg: a wizard for creating a new member accounts)</em></li>
	<li>What is the minimum acceptable load time for data intensive pages <em>(eg: a report, or complex searches across the database)</em></li>
	<li>How quickly do you expect the site to grow? <em>(eg: 2000 users within 12 months, 1M photos within 3 years)</em></li>
</ul>
<h3>Security</h3>
<ul>
	<li>Will we be managing sensitive information? <em>(eg: passwords, bank account/credit card information, etc.)</em></li>
	<li>What are the requirements for encrypting data sent over the public Internet? <em>(eg: checkout process involving credit card transactions)</em></li>
	<li>What are the requirements for restricting physical access to the hardware?  <em>(eg: sealed cabinet at hardened telco hotel)</em></li>
	<li>Is a shared hardware hosting plan acceptable, or are physically separate servers required?</li>
	<li>Is operating system access control of network resources sufficient, or is a separate hardware firewall device required?</li>
	<li>What security breaches should we develop contingency plans for?  <em>(eg: customer account compromised, theft of physical server)</em></li>
	<li>Are there any specific security regulations that may apply to this project? <em>(eg: PCI-DSS, government security clearance)</em></li>
</ul>
<h3>Integration</h3>
<ul>
	<li>Will this system interact with any other systems? <em>(eg: credit card gateway, LDAP server, Google Maps)</em></li>
	<li>What contingency provisions should we have if those systems are not reachable?</li>
	<li>Will this system provide services for other systems? <em>(eg: this system provides single sign on, or web services for accessing data)</em></li>
</ul>
<h3>Environment</h3>
<ul>
	<li>Does your company have any specific requirements around languages, protocols, or deployment environments? <em>(eg: Oracle database server, Java EE 5)</em></li>
</ul>
<h3>Documentation</h3>
<ul>
	<li>How comprehensive should the technical documentation be?  <em>(eg: inline comments in the source code, UML modeling, interaction diagrams, API documentation, etc.)</em></li>
</ul>
Anyone have other things to contribute?
