## Whiskermania: An Intro to Network Concepts: Section 4: The Picture Emerges<br>
### **Summary**<br>
Morgan gets pulled away again. Something about a server issue and a volunteer who accidentally unplugged the wrong thing.
<br><br>
"Can you hold down the fort? I'll be back in an hour."
<br><br>
You're alone with the data, Jamie's notes, and Biscuits, who has curled up on the warm part of the desk near the monitor. Time to investigate properly.
<br><br>
Let's start where Jamie left off: that suspicious external IP. If anyone connected to 185.174.137.42, they had to look up the domain first. DNS will tell us what domain points to that IP.
<br><br>

**Q1. What domain resolves to 185.174.137.42?**<br><br>

```
DnsEvents
| where resolved_ips has "185.174.137.42"
| distinct query_name
```
<br>

**Answer: update-cdn-service.xyz**<br>

**Q2. How many distinct internal IPs queried this domain?**<br><br>

```
DnsEvents
| where query_name contains "update-cdn-service.xyz"
| distinct client_ip
```
<br>

**Answer: 3**<br>

**Q3. Is update-cdn-service.xyz an internal domain or an external domain?**<br>

```
DnsEvents
| where query_name contains "update-cdn-service.xyz"
| summarize count() by client_ip
| order by count_ desc
```
<br>

**Answer: external**<br>

**Q4. What destination port is this traffic using?**<br>

```
NetworkFlow
| where dest_ip == "185.174.137.42"
| project timestamp, src_ip, dest_ip, dest_port, protocol, bytes
| take 10
```
<br>

**Answer: 443**<br>

**Q5. What protocol normally runs on port 443?**<br>

**Answer: HTTPS**<br>

**Q6. What URL path appears repeatedly in these requests?**<br>

```
ProxyEvents
| where domain == "update-cdn-service.xyz"
| project timestamp, src_ip, url, method, status_code
| order by timestamp asc
```
<br>

**Answer: /api/v1**<br>

**Q7. What does C2 stand for?**<br><br>

**Answer: Command and Control**<br><br>

**Q8. What is the term for malware regularly checking in with its C2 server?**<br><br>

**Answer: beaconing**<br><br>

**Q9. Type all good here to continue.**<br><br>

**Answer: all good here**<br><br>

**Q10. What domain in the sender address is impersonating the sanctuary?**<br><br>

```
Email
| where sender !endswith "@whiskersandwonders.org"
| where sender contains "whiskersandwonders"
| project timestamp, sender, recipient, subject
```
<br>

**Answer: whiskersandwonders-hr.com**<br><br>

**Q11. What was the subject line of the phishing email?**<br><br>

```
Email
| where sender contains "whiskersandwonders-hr.com"
| project timestamp, sender, recipient, subject
```
<br>

**Answer: [EXTERNAL] Important: Employee Benefits Update Required**<br><br>

**Q12. How many employees received the phishing email?**<br><br>

```
Email
| where sender contains "whiskersandwonders-hr.com"
| distinct recipient
```
<br>

**Answer: 3**<br><br>

**Q13. Did all three phishing recipients become compromised? (yes/no)**<br><br>
Using the queries provided.<br><br>

```
// Get phishing recipients
Email
| where sender contains "whiskersandwonders-hr.com"
| distinct recipient
```
<br>
3 emails are returned from the above query

- alex_rivera@whiskersandwonders.org
- jessica_huang@whiskersandwonders.org
- david_okonkwo@whiskersandwonders.org


```
// Compare to C2 DNS queries
DnsEvents
| where query_name contains "update-cdn-service.xyz"
| distinct client_ip
```
<br>
3 IP addresses are returned that contacted the C2.<br><br>

- 10.10.16.14
- 10.10.16.7
- 10.10.16.24

Comapre these IP addresses to the emails / users from the first query using the Employee table. Can see that the IP addreses match the email addresses.<br><br>

**Answer: yes**<br><br>

**Q14. Type jamie was right to continue.**<br><br>

**Answer: jamie was right**<br><br>

**Q15. What date was the first phishing email sent? (copy and paste)**<br><br>

```
Email
| where sender contains "whiskersandwonders-hr.com"
| project timestamp, recipient
| order by timestamp asc
```
<br>

**Answer: 6/2/2025, 4:00:00 PM**<br><br>

**Q16. Approximately how many hours between the phishing email and the first C2 beacon?**<br><br>

```
DnsEvents
| where query_name contains "update-cdn-service.xyz"
| summarize first_query=min(timestamp) by client_ip
| order by first_query asc
```
<br>
The C2 traffic started at 6/2/2025, 11:52:31 PM, compare it with when the first phising email was sent at 6/2/2025, 4:00:00 PM.<br><br>

**Answer: 7**<br><br>

**Q17. How many requests did the victim computer make to the malicious domain?**<br><br>

```
ProxyEvents
| where domain == "update-cdn-service.xyz"
| project timestamp, src_ip
| order by timestamp asc
```
<br>

**Answer: 6**<br><br>

**Q18. What is the C2 domain?**<br><br>

```
DnsEvents 
| where query_name contains "update-cdn-service.xyz" 
| distinct query_name
```
<br>

**Answer: update-cdn-service.xyz**<br><br>

**Q19. What is the C2 IP address?**<br><br>

```
DnsEvents 
| where query_name == "update-cdn-service.xyz" 
| distinct tostring(resolved_ips)
```
<br>

**Answer: 185.174.137.42**<br><br>

**Q20. What is the phishing sender domain?**<br><br>

```
Email 
| where sender contains "whiskersandwonders-hr" 
| distinct sender
```
<br>

**Answer: whiskersandwonders-hr.com**<br><br>

**Q21. What destination port is the C2 traffic using?**<br><br>
Using the IP address from  question 19.<br><br>

```
NetworkFlow
| where dest_ip == "185.174.137.42"
```
<br>

**Answer: 443**<br><br>

**Q22. What is the name of the compromised Development Officer?**<br><br>

```
DnsEvents
| where query_name contains "update-cdn-service.xyz"
| distinct client_ip
| join kind=inner (Employees | project ip_addr, name, username, role) on $left.client_ip == $right.ip_addr
| project name, username, role
```
<br>

**Answer: Alex Rivera**<br><br>

**Q23. What role do two of the compromised users share?**<br><br>

```
DnsEvents
| where query_name contains "update-cdn-service.xyz"
| distinct client_ip
| join kind=inner (Employees | project ip_addr, name, role) on $left.client_ip == $right.ip_addr
| project name, role
```
<br>

**Answer: Adoption Coordinator**<br><br>

**Q24. Type they want the money to continue.**<br><br>

**Answer: they want the money**<br><br>

**Q25. What domain should be blocked at DNS?**<br><br>
**Answer: **<br><br>


