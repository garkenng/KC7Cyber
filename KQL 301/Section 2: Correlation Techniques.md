## KQL 301: Section 2: Correlation Techniques<br>

**Q1. Type 'let's improve this' to carry on.**<br><br>

**Answer: let's improve this**<br><br>

**Q2. Enter more power to continue.**<br><br>

**Answer:  more power**<br><br>

**Q3. How many employees clicked the phishing link?**<br><br>

```
let victim_ips =     
    ProxyEvents
    | where domain in ("api-sync-updates.top", "update-cdn-service.xyz")
    | distinct src_ip;
Employees
| where ip_addr in (victim_ips)
```
<br>

**Answer: 3**<br><br>

**Q4. Who was the first person to click on a link to the malcious domain? (name)**<br><br>

```
ProxyEvents
| where domain in ("api-sync-updates.top", "update-cdn-service.xyz")
| lookup Employees on $left.src_ip == $right.ip_addr
| project-reorder timestamp, src_ip, name
```
<br>

**Answer: David Okonkwo**<br><br>

**Q5. No question**<br><br>

**Answer: Nothing to answer**<br><br>

**Q6. You are joining Employees data (your enrichment data) against Authentication data (you main) data to see the names of accounts that were compromised. Which table is the left table?**<br><br>

**Answer: Authentication**<br><br>

**Q7. Two employees received links to update-cdn-service.xyz. What is the first email recipient's IP address?**<br><br>

```
Email
| where sender == "noreply@whiskersandwonders-hr.com"
| lookup Employees on $left.recipient == $right.email_addr
| project-reorder timestamp, sender, recipient, ip_addr
```
<br>

**Answer: 10.10.16.7**<br><br>

**Q8. What is the hostname of the last employee to receive an email matching this pattern?**<br><br>

```
Email
| where links has "aspca.org"
| lookup Employees on $left.recipient== $right.email_addr
| project timestamp, hostname
```
<br>

**Answer: IIHO-DESKTOP**<br><br>

**Q9. Which role received the most emails from aspca.org**<br><br>

**Answer: **<br><br>

**Q10. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

