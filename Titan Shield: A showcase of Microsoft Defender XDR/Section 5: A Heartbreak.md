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

**Q9. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>

