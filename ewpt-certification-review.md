---
description: eLearnSecurity Web Application Penetration Tester Certification Review
cover: .gitbook/assets/ewptnewmobile.png
coverY: 238.95802469135805
---

# 🕸 eWPT Certification Review

So I bought this voucher because it was Prime day and it was half off, so $200 instead of $400. It just made it more affordable for a student like me. I am in the middle of prepping for the eCPPTv2, also from eLearnSecurity, and so I figured this couldn't hurt.

So lets get to the meat of this review. You want to know what me, a somewhat experienced web and API hacker, think of the eWPT exam process. Well it was smooth one. I love they stick with OpenVPN to connect to the environment unlike some other certifying bodies, cough cough... EC-Council. I had two connection drops during my exam process and both were because I was running two gobuster instances simultaneously, I was desperately checking for subdomains.

So to start with this exam is a classic black box pentest on the website that your given in the letter of engagement. If you have ever done a web assessment just complete it exactly how you normally would. It is kinda dated, made \~2015, but that's pretty realistic for a lot of sites I have assessed.

Because this is an actual assessment you are doing you will have to check everything, and I mean everything. There are a lot of small issues that you won't find if you just try to pwn the website like in a CTF. Also because this is an actual assessment take A LOT of notes and screenshots. This will save you a lot of time writing your report.

So because this is a web assessment don't be expecting to pop shells left and right. They have it pretty locked down and so to maneuver is very different than it is when you can grab a reverse shell. You will need to know how the back end works and what pieces work with what. This took a lot of thinking on my part. I expected to be done in one night, and I would have if it was like HackTheBox or TryHackMe but it just isn't.&#x20;

Another problem I had during the exam was doubting myself. There is a set goal you need to accomplish along with the regular assessment and I was sure that I had not accomplished it for two days. It not as straight forward as popping a shell and priv-escing to root. You know you have the highest level privilages and role but is this the right area, could there be another subdomain somewhere, another directory not in my wordlist? No, you will know when you have found that area and when you get the correct roles needed to satisfy the letter of engagement criteria.

So for anyone planning on taking the exam here are my tips:

* Notes on everything no matter what
* Screenshots of each step and vulnerability found
* Writeup even the low findings, like out-of-date versions
* Know how to use SQLMap, its your friend.

```
sqlmap -r <request>.txt
```

* Learn basics of SQL syntax and PHP

Overall I learned a good amount from this exam. Especially with crafting my own payloads to get around obstacles blocking you from the normal route an attacker would take. Its not 100% realistic but it does a good job for what its worth and gives you a nice boost in confidence.

