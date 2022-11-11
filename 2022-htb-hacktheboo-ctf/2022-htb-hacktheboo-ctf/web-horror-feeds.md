---
description: 2022 HTB HackTheBoo CTF - Web - Horror Feeds
---

# Web - Horror Feeds

Now this was a tricky challenge. It was rated easy but was definetly more of a medium challenge.

To start we got the back end of the website and a link to the site we spun up. Skimming through you could identify this was going to be an SQL injection attack almost right away and I found the injection point pretty soon after realizing this.

The injection point was located in the register API call for the site. In order to exploit this I turned to good ol' SQLmap. Capturing a register request with Burpsuite, I saved it as a txt file and passed it to SQLmap:

```
sqlmap -r req.txt --level=3 --risk=3 --dbs
```

After letting it run for a few minutes it found a solid injection in the username field. Using this I was able to dump data but when I went to dump the user database, SQLmap had filled it up with nonsense as it was testing it. To work around this I just executed a MySQL query to grab the hash of the user 'admin'. This worked but the hash in the database was invalid. So even if you had the password for admin it would error out and not let you login as its not a valid bcrypt hash.

Now this took me a little to figure out but eventually I got a solution, I was going to write my own hash for admin into the database. SQLmap couldn't do this though. I needed to write my own custom query. Luckily we had access to the database and knew what tables there were and so after a few hours of trial and error, and a lot of google, I got a working SQLI:

```sql
test"="test" AND (1+1) or 'test',"test2") UNION ALL select 'admin','test' ON DUPLICATE KEY UPDATE password = '$2a$12$ZxNKpqgT1kBsIKIT1Nt0huQcAUMuBO2fqsNbEoHMHvHcWluyMla4i' -- -
```

This payload added the bcrypt hash, this one is the hash for 'test', to the database for admin. Now, using the login page, I could login with 'admin' and the password 'test' and boom, I had the flag!

PWNED!
