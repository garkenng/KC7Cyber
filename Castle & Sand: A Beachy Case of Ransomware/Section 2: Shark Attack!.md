## Castle & Sand: A Beachy Case of Ransomware: Section 2: Shark Attack!<br>
### **Summary**<br>
<p>
Oh no! Castle&Sand has been hit with ransomware!!! They posted a ransom note and locked all of the company's files. IT was able to get you a copy of the ransom note. Take a look at the note.
</p>


**Q1. What email address did the threat actor provide to Castle&Sand to communicate with them?**<br><br>

**Answer:  sharknadorules_gang@onionmail.org**<br><br>

**Q2. What is the unique decryption ID?**<br><br>

**Answer:  SUNNYDAY123329JA0**<br><br>

**Q3. Should this be something you post publicly about? Yes or no?**<br><br>

**Answer: No**<br><br>

**Q4. The ransom note filename was called PAY_UP_OR_SWIM_WITH_THE_FISHES.txt. How many notes appeared in Castle&Sand's environment?**<br><br>

```
FileCreationEvents
| where filename == "PAY_UP_OR_SWIM_WITH_THE_FISHES.txt"
| count 
```
<br>

**Answer: 774**<br><br>

**Q5. How many distinct hostnames had the ransom note?**<br><br>

```
FileCreationEvents
| where filename == "PAY_UP_OR_SWIM_WITH_THE_FISHES.txt"
| distinct hostname 
| count
```
<br>

**Answer: 774**<br><br>

**Q6. How many distinct employee roles were affected by the ransomware attack?**<br><br>

```
let DistinctRoles =
FileCreationEvents
| where filename == "PAY_UP_OR_SWIM_WITH_THE_FISHES.txt"
| distinct hostname;
Employees
| where hostname in (DistinctRoles)
| distinct role
```
<br>

**Answer: 18**<br><br>

**Q7. How many unique hostnames belong to IT employees?**<br><br>

```
let DistinctRoles =
FileCreationEvents
| where filename == "PAY_UP_OR_SWIM_WITH_THE_FISHES.txt"
| distinct hostname;
Employees
| where hostname in (DistinctRoles)
| where role has "IT"
| distinct hostname
```
<br>

**Answer: 25**<br><br>

**Q8. One of the IT employees has an IP address that ends in .46. What is that employee's name?**<br><br>

```
Employees
| where ip_addr contains ".46"
| where role has "IT"
```
<br>

**Answer: Simeon Kakpovi**<br><br>

**Q9. How many security alerts involved the different hosts?**<br><br>

```
let impact_hosts = FileCreationEvents
| where filename == 'PAY_UP_OR_SWIM_WITH_THE_FISHES.txt'
| distinct hostname;
SecurityAlerts
| where description has_any (impact_hosts)
```
<br>

**Answer: 652**<br><br>

**Q10. How many Security Alerts reference the hostnames of helpdesk employees that received ransom notes?**<br><br>

```
let impact_hosts = FileCreationEvents
| where filename == 'PAY_UP_OR_SWIM_WITH_THE_FISHES.txt'
| distinct hostname;
let helpdesk_hostnames = Employees
| where hostname in (impact_hosts)
| where role contains "IT Helpdesk"
| distinct hostname;
SecurityAlerts
| where description has_any (helpdesk_hostnames)
```
<br>

**Answer: 27**<br><br>

**Q11. Let's look for any anomalies in the alerts that look different from the other alerts and might be shark-themed like the ransomware. You should find one. Who owns the machine that was flagged on that alert? (provide their name)**<br><br>

<p>
  One result stands out. Under the description.
</p>

```
A suspicious file was quarantined on host 6S7W-MACHINE: Chomping-Schedule_Changes.xlsx
```
<br>

```
Employees
| where hostname == "6S7W-MACHINE"
```
<br>

**Answer: Preston Lane**<br><br>

**Q12. When did the file appear on that user's machine? (copy and paste the full timestamp)**<br><br>

```
FileCreationEvents
| where hostname == "6S7W-MACHINE"
| where path has "Chomping-Schedule_Changes.xlsx"
```
<br>

**Answer: 2023-05-26 09:26:15+00:00**<br><br>

**Q13. What's the SHA256 hash of that file?**<br><br>

**Answer: 71daa56c10f7833848a09cf8160ab5d79da2dd2477b6b3791675e6a8d1635016*<br><br>

**Q14. What application created that file?**<br><br>

**Answer: firefox.exe**<br><br>

**Q15. How many unique hosts had files with that exact name on their systems?**<br><br>

```
FileCreationEvents
| where path contains "Chomping-Schedule_Changes.xlsx"
| distinct hostname
| count
```
<br>

**Answer: 15**<br><br>

**Q16. How many unique domains did employees download this file from?**<br><br>

```
OutboundNetworkEvents
| where url contains "Chomping-Schedule_Changes.xlsx" 
| distinct url
```
<br>

**Answer: 2**<br><br>

**Q17. Based on the employee we've been tracking from Question 11, which domain did they download the file from?**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.2.1"
| where url contains "Chomping-Schedule_Changes"
```
<br>

**Answer: jawfin.com**<br><br>

**Q18. How many unique IP addresses did the domain resolve to?**<br><br>

```
PassiveDns
| where domain contains "jawfin.com"
| distinct ip
| count
```
<br>

**Answer: 6**<br><br>

**Q19. Which IP address is closest in time to when the file was created of the employee's machine?**<br><br>

```
PassiveDns
| where timestamp > datetime(05-25-2023 16:40)
| where domain contains "jawfin.com"
```
<br>

**Answer: **<br><br>

**Q20. There was another domain found from Q16. How many unique IPs did that domain resolve to?**<br><br>

```
PassiveDns
| where domain contains "sharkfin"
| distinct ip
```
<br>

**Answer: 4**<br><br>

**Q21. Let's take all of the IP addresses from the two domains and search them against network events on Castle&Sand's website. How many records returned from your query?**<br><br>

```
let NetworkEvents = PassiveDns
| where domain contains "jawfin.com" or domain contains "sharkfin"
| distinct ip;
InboundNetworkEvents
| where src_ip in (NetworkEvents)
```
<br>


**Answer: 39**<br><br>

**Q22. When was the first time we saw any of these actor IP addresses from Q21 against Castle&Sand's network?**<br><br>

```
let ActorIP = PassiveDns
| where domain contains "jawfin.com" or domain contains "sharkfin"
| distinct ip;
InboundNetworkEvents
| where src_ip in (ActorIP)
```
<br>

**Answer: 2023-05-20 03:11:57+00:00**<br><br>

**Q23. Let's search the actor IPs against AuthenticationEvents to see if they logged into any user machines or email accounts. How many records did you get back?**<br><br>

```
AuthenticationEvents
| where src_ip == "157.242.169.232"
```
<br>

**Answer: 0**<br><br>

**Q24. Let's look for the malicious domains in Emails. How many records did you get back?**<br><br>

```
Email
| where link contains "jawfin" or link contains "sharkfin"
| count
```
<br>

**Answer: 14**<br><br>

**Q25. When was the earliest email sent?**<br><br>

```
Email
| where link contains "jawfin" or link contains "sharkfin"
```
<br>

**Answer: 2023-05-25 16:33:09+00:00**<br><br>

**Q26. Who was the sender?**<br><br>

**Answer: legal.sand@verizon.com**<br><br>

**Q27. How many emails total did that sender send to Castle&Sand employees?**<br><br>

```
Email
| where sender == "legal.sand@verizon.com"
```
<br>

**Answer: 23**<br><br>

**Q28. Take all of the distinct sender or reply_to emails from the last question. How many emails total are associated with these email addresses?**<br><br>

```
let EmailAddresses = Email
| where sender == "legal.sand@verizon.com"
| distinct reply_to;
Email
| where sender in (EmailAddresses) or reply_to in (EmailAddresses)
```
<br>

**Answer: 40**<br><br>

**Q29. How many unique domains did the email addresses use in their emails?**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

