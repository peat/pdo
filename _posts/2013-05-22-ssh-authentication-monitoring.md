---
layout: post
title: sshame - SSH Authentication Monitoring
tags:
status: publish
type: post
published: true
meta: {}
---
I wrote a little tool this morning to help get rid of a common system administration nuisance: lazy bots that port scan for SSH servers, then attempt brute force attacks on common accounts and passwords.

The tool, called [sshame](https://github.com/peat/sshame), is pretty simple. It scans sshd log files for failed user logins, and lists out any IP addresses that rise above a given threshold. If I get curious, it also lets me inspect how many attempts were made, and for which user accounts.

For example, if I want to highlight the IP addresses which have made at least ten failed attempts:

```bash
$ cat /var/log/auth.log | sshame -t 10
221.176.53.74
129.194.160.23
61.142.106.34
```

In any case, I regenerate the blacklist every hour and feed the addresses into my firewall rules. It's not foolproof by any means, but it helps keep the script kiddies off my lawn.

And yes, the example IP addresses above are from repeated attempts originating in China and Switzerland. :)

The [source and documentation](https://github.com/peat/sshame) for sshame is all available on GitHub. Have fun!