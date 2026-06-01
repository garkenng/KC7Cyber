## CloutHaus: Social Media leads to Compromise: Got Clout<br>
### **Summary**<br><br>
Okay team, things just got real. 😰
<br><br>
- 1 hour after Afomiya clicked a phishing link, someone logged into her company email.
- Different device. Different country. Using an ancient Internet Explorer build (yes, really).
- This isn’t casual snooping - it’s email compromise, recon, and possible data theft.

Your mission: use the Authentication, Network, and Email logs to uncover what the intruder did, what they wanted, and what may be gone. Be methodical. Document everything 🕵️‍♀️
<br><br>
Start here:
<br><br>
Find the suspicious login event.
Identify the IP address used to gain access.
Trace actions from that session (reads/sends, forwarding rules, downloads).
<br><br>

**Q1 What IP address was used to gain access?**<br><br>

```
AuthenticationEvents
| where description has "email"
| where user_agent has "MSIE"
| where timestamp > datetime(4/3/2025, 12:00:00)
| where timestamp < datetime(4/3/2025, 13:00:00)
```
<br>

The first result that the query returns looks of interest. The IP address is not from a local machine and co-insides with the time frame of when the email login attempt would have been made.<br><br>

**Answer: 182.45.67.89**<br><br>

**Q2 What domains are associated with this IP? (enter one)**<br><br>

```
PassiveDns
| where ip == "182.45.67.89"
```
<br>
Two unqiue omains 

**Answer: influencer-deals.net or dior-partners.com**<br><br>

**Q3 What part of the User-Agent string indicates the suspicious browser and operating system? (Submit either the browser name/version or the operating system name/version.)**<br><br>



