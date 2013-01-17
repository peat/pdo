---
layout: post
title: OpenSolaris on Amazon EC2 Review
tags:
- Amazon
- Beta
- EC2
- OpenSolaris
- Project Indiana
- Sun
status: publish
type: post
published: true
meta:
  _edit_last: '2'
---
I spent some time playing with <a href="http://www.sun.com/third-party/global/amazon/index.jsp">OpenSolaris on EC2</a> this weekend, and I'm a bit disappointed — partially because of OpenSolaris, and partially because of how the beta program was set up.

But, good news first.  I'm glad to see Project Indiana released, and EC2 is an easy way to take it for a test drive.  All of the packages I tinkered with could be <a href="http://en.wikipedia.org/wiki/DTrace">DTraced</a> to my heart's content, and it's definitely a great improvement for debugging and monitoring of apps in the EC2 environment.

Bad news?  First, all of the beta instances I booted were very slow.  I'm sure this has to do with the provisioning of hardware for the beta program, and not with OpenSolaris itself.  The beta servers are separate from the main Amazon servers, and I expect the speed will be on par with Linux when the beta period ends.  Regardless, it does make the experience pretty frustrating.

Second, OpenSolaris openly touts their great package manager, but the selection of packages downright sucks compared to the Linux distros available on EC2.  If you're deploying anything more than a basic web stack on OpenSolaris, you're going to be building a lot of software by hand, and that can be a frustrating experience on any Solaris.

Regardless, I could get PHP and Rails apps humming along just fine (although I've had a lot of practice).  While OpenSolaris feels stable and DTrace is great, I spent way more time getting a system up to speed than I would have with Ubuntu or CentOS.  The over-utilized servers didn't help much either.

I do have hope for the future, tough.  None of the issues demonstrated fundamental flaws in OpenSolaris or EC2, and I expect all of these problems to be fixed in time.  The OpenSolaris team has obviously put a lot of work into this release, and I'm looking forward to seeing how the platform evolves.

One thing I haven't been able to play with is ZFS.  I'm interested in benchmarking ZFS on the persistent storage service, and a little excited to see what happens when several storage reservations are ganged up into a single ZFS pool ... although I'm not going to go anywhere near that situation until the basic performance issues are resolved!

<strong>Update</strong>: I just wanted to clarify the package situation — the shortage of packages is only on the basic EC2 image for OpenSolaris 2008.05, <em>not</em> on the standard distribution you download from the OpenSolaris site.

<strong>Update:</strong> I had a follow up call with the OpenSolaris on EC2 team.  <a href="http://peat.org/2008/05/18/opensolaris-on-amazon-ec2-part-ii/">More thoughts here</a>.
