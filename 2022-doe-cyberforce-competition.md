---
description: 2022 Department of Energy Cyberforce Competition Overview
cover: .gitbook/assets/cyberforce.jpg
coverY: 227.98232695139913
---

# ☀ 2022 DOE Cyberforce Competition

This past weekend myself and five other members of the Virginia Tech Corps of Cadets Cyber Team competed in the DOE Cyberforce competition and placed 22nd out of 141 active teams from other schools around the nation. This is a defensive focused competition that allowed our team to gain experience in a large variety of roles, from incident response and security architecture, to audit and policy. This was a great learning opportunity for me as I have been mainly on the red team side of the aisle but now I got to actively respond to an attack.

### Preparation&#x20;

A few weeks out from the competition we got an email containing the rules and expectations for the competition. This told us basically what we needed to do to get the most points. Two parts of the scoring were the C-Suite brief and Security Documentation. Both of these tasks needed to be completed before we left for the competition so we had to start on them right when we got the infrastructure, about three weeks out.

The security documentation was the first part we completed and it was relatively straightforward. It involved creating a network diagram as well as listing all machines with what ports were open and what services were running on them. It also wanted a list of all vulnerabilities we could find in each and how we would remediate them. We ended up finding over 45 vulnerabilities which seems to be close to the amount that they were looking for.

Now that we had the security documentation done we could use what we learned from doing that research in the C-Suite briefing. The briefing was pretty straight forward and we just outlined the situation, the problems, our solutions to said problems, and a conclusion. Standard high level brief.

The final piece of preparation, that came out of the blue, was the website. We received a document that outlined what they wanted from the website, linked below:

{% file src=".gitbook/assets/CFC_Blue_Team_Website_Requirements_2022.pdf" %}

I took the role of creating this lovely website. These guidelines wanted a somewhat nice looking website that integrated with an FTP server, an SMTP server, and a MYSQL server. This was two weeks out from the competition and I had class, hw, an exam, and ROTC training so I was thrilled. After some long hours and stressful nights I got it done and the final product is linked below: (ignore the hard coded creds and me using a dev server in production) [https://github.com/gsmith257-cyber/flask\_siteDOE](https://github.com/gsmith257-cyber/flask\_siteDOE)

Now we had everything done we needed right? Wrong! We had to setup logging on each server!

I decided the best way to do this quickly would be to use auditd and rsyslog. We created an rsyslog server on our blueteam instance and configured rsyslog on all the Linux machines to direct all logs to it. For our auditd rules we used: [https://github.com/Neo23x0/auditd/blob/master/audit.rules](https://github.com/Neo23x0/auditd/blob/master/audit.rules) . On the Windows machines we used Rsyslog Client to do the same thing. Also on the windows machines we downloaded and setup chainsaw, a powerful tool that parses windows event logs, to hunt on the machine itself.

Now that we had all the data flowing in we needed a way to manage it, a SIEM. I settled on a easy to setup and configure tool available on GitHub named LogESP, linked here: [https://github.com/dogoncouch/LogESP](https://github.com/dogoncouch/LogESP) . This allowed me to customize some regex rules to handle the auditd logs and help me sort through them better as they came in.

Now, looking back, we should have used a program like Splunk (free trial) or RedELK to do all this as they have a lot better data visualization for the large amount of data coming in but we finished setting up LogESP the night before the competition so there wasn't much time.

### During the Competition

Now its competition day! We have everything setup and ready to go, our website is working, we have logs flowing in, Wireshark was up and running, all looks well. I get a ping from our red team member asking if I am ready for the first attack chain, I am doing incident response alone as the rest of the team focused on the anomolies (CTF problems). I replied 'yessir' and a few seconds later I see a shell being opened on a machine. The logs are working! I can carefully follow through each binary they touched and what arguments they used as well as suspicious network activity and file reading/writing. This allowed me to track this chain through the Linux machine but when the time was up, we had one hour to respond, I didn't get full points... I had missed the attacker getting into one of the windows machines.

I found the problem was there was too much to look through in windows event logs and I needed something simpler to get straight to the point. To solve this I configured the group policy to store powershell transcripts to a log folder we could checkout. This allowed me to see exactly what the attacker was running over WinRM, what they were using to connect. This also saved me time to more methodically look through the event logs chainsaw gave me and find anything else happening.

The next few attack chains went a lot smoother and by the last one I had figured everything out and got a perfect score! In the four chains I completed I got a 90, 90, 120, and 150 (all out of 150). Not bad for a red teamer trying to blueteam for the first time.

My teammates did great on the anomalies and we placed well. This was our first time so almost top 15% is good in my book.



Hope you had an informative read and picked up something new from it!
