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
The query from question 1, the first result under user agent returns the folloing:<br><br>

```
Mozilla/5.0 (compatible; MSIE 5.0; Windows NT 5.2; Trident/4.1)
```
<br>

Based on MSIE which is Microsoft Internet Explorer 5.0 released in 1999 and Windows NT 5.2 which is Windows XP released in 2003. The user is using an outdated browser and OS.<br><br>

**Answer: MSIE 5.0 or Windows NT 5.2**<br><br>

**Q4 What country did the login originate from?**<br><br>
Using website iplocation.net with the IP address from question 2. The IP address originates from Shandong, China.<br><br>

**Answer: China**<br><br>

**Q5 According to the attacker's web search history on the site, what were they trying to hack?**<br><br>

```
InboundNetworkEvents
| where src_ip == "182.45.67.89"
```
<br>

Scrolling through the results, one url search history is of interest.<br><br>

```
https://clouthaus.com/search=How+to+hack+an+influencer's+location+from+their+Instagram+story
```
<br>

**Answer: Location**<br><br>

**Q6 According to another search log, what kind of personal info were they sneakily trying to uncover (and pretending to ask “for a friend”)?**<br><br>
Looking at the url search history again. The answer can be found.<br><br>

**Answer: home address**<br><br>

```
https://clouthaus.com/search=Afomiya+Storm+home+address??+(asking+for+a+friend)
```
<br>

**Answer: home address**<br><br>

**Q7  What kind of account or app does that log suggest they were targeting?**<br><br>

```
https://clouthaus.com/search=Afomiya's+Venmo+history+–+is+that+public??
```
<br>

**Answer: Venmo**<br><br>

**Q8 Based on another search, what shady and fake event were they pretending to plan as a way to lure Afomiya?**<br><br>

```
https://clouthaus.com/search=How+much+would+it+cost+to+hire+Afomiya+for+a+fake+birthday+party?
```
<br>

**Answer: Birthday Party**<br><br>

**Q9 What external email address received messages forwarded from Afomiya’s account?**<br><br>
To search for email addresses that were forwarded from Afomiya account, there are four fields that can be searched to narrow the result done. The email was sent externally, sent from Afomiya, external email address is not internal (will not contain the domain clouthaus) and sent after the phising email was clicked on 04/03/2025 12:20.

```
Email
| where subject has "external"
| where sender contains "afomiya"
| where recipient !contains "clouthaus.com"
| where timestamp >= datetime(4/3/2025, 12:20:00)
```
<br>

**Answer: noreply@influencer-deals.net**<br><br>




