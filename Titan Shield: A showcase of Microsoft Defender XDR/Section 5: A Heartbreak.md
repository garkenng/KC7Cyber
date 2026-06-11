## Titan Shield: A showcase of Microsoft Defender XDR: Section 5: A Heartbreak<br>
### **Summary**<br>
You look through the logs, and it doesnt seem like Taylor went out of his way to search and download this file. Maybe he just clicked a link in an email.
<br><br>
Let's look for this URL to see if it was delivered in any emails.
<br><br>


**Q1. Who sent the email?**<br><br>

```
Email
| where link has "https://healthylifestyle.com/share/New_Diet_Plan_For_My_Love.xlsx"
```
<br>

**Answer: marcella_flores@gmail.com**<br><br>

**Q2. What was the subject of that email?**<br><br>
From previous query.<br><br>

**Answer: [EXTERNAL] RE: Relax with these yoga poses, baby! 🧘‍♂️**<br><br>

**Q3. Type she's just not that into you to continue**<br><br>

**Answer: she's just not that into you**<br><br>

**Q4. How many emails did marcella_flores@gmail.com send?**<br><br>

```
Email
| where sender == "marcella_flores@gmail.com"
| count
```
<br>

**Answer: 13**<br><br>

**Q5. How many total domains were in the links seen in that email?**<br><br>

```
Email
| where sender == "marcella_flores@gmail.com"
| extend domain = parse_url(link).Host
| distinct tostring(domain)
```
<br>

**Answer: 5**<br><br>

**Q6. Let's search all three of those domains in the Microsoft Defender XDR Threat Intelligence Portal to see if we can get some attribution details!. Which threat actor is one of these domains linked to?**<br><br>

**Answer: Crimson Sandstorm**<br><br>


**Q7. Look in PassiveDNS. How many IPs did these domains resolve to?**<br><br>

```
PassiveDns
| where domain in ("outlook-services.com","healthylifestyle.com")
| distinct ip
```
<br>

**Answer: 2**<br><br>


**Q8. If the actor conducted reconnaisance against our company, which table would we find that activity in?**<br><br>

**Answer: InboundNetworkEvents**<br><br>

**Q9. Let's use this query to investigate the activity in this table. How many results did you find?**<br><br>

```
InboundNetworkEvents
| where src_ip in ("208.199.30.154","202.241.233.180")
```
<br>

**Answer: 47**<br><br>

**Q10. When did the recon from threat actor IPs begin? (copy and paste the full timestamp from the logs)**<br><br>
First result from previous query.<br><br>

**Answer: 7/5/2024, 12:00:00 AM**<br><br>

**Q11. Which social media platform were they using to conduct this recon?**<br><br>
Looking at the referrer column from query 9.<br><br>

**Answer: LinkedIn**<br><br>


**Q12. Which employee did the threat actor exfiltrate data from?**<br><br>

```
Email
| where subject contains "data exfiltration"
```
<br>
The sender email address that exfiltrate date is david_jackson@titanshield.com.

**Answer: David Jackson**<br><br>


**Q13. What address did the actor send the exfiltrated data to?**<br><br>
From previous query.<br><br>

**Answer: exfilbucket93@gmail.com**<br><br>

**Q14. What is this user's IP address?**<br><br>

```
Employees
| where name contains "David jackson"
```
<br>

**Answer: 10.10.0.8**<br><br>

**Q15. The browsing logs might help us better understand what happened with this user. When (enter full timestamp) did David Jackson make a google search about EDR alerts?**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.8"
| where url contains "edr"
```
<br>

**Answer: 8/3/2024, 7:09:23 AM**<br><br>


**Q16. On which days of the week does David's girlfriend not talk to him? (Enter your answer in order of the days, separated by a comma - example: Sunday,Funday)**<br><br>

**Answer: ready**<br><br>




**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>

