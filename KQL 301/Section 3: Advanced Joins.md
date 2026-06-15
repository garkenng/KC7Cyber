## KQL 301: Section 3: Advance Joins<br>

**Q1. Click Submit to continue**<br><br>

**Q2. How many results do we get back after the join?**<br><br>

```
Email
| where sender == "diego_hernandez@whiskersandwonders.org"
| join kind=leftouter Employees on $left.recipient == $right.email_addr
| project-reorder timestamp, sender, recipient, ip_addr
```
<br>

**Answer: 15**<br><br>

**Q3. How many results do we get back now?**<br><br>

```
Email
| where sender == "diego_hernandez@whiskersandwonders.org"
| join kind=inner Employees on $left.recipient == $right.email_addr
| project-reorder timestamp, sender, recipient, ip_addr
```
<br>

**Answer: 7**<br><br>

**Q4. How many results do we get back this time?**<br><br>

```
Email
| where sender == "diego_hernandez@whiskersandwonders.org"
| join kind=rightouter Employees on $left.recipient == $right.email_addr
| where isempty(sender)
| project name, email_addr
```
<br>

**Answer: 30**<br><br>

**Q5. What percent of users clicked on the link?**<br><br>

```
Email
| where links has "update-cdn-service.xyz"
| mv-expand links to typeof(string)
| join kind=leftouter Employees on $left.recipient == $right.email_addr
| join kind=leftouter (    
    ProxyEvents
    | where url has "update-cdn-service.xyz"
) on $left.ip_addr == $right.src_ip, $left.links == $right.url
| project timestamp, sender, recipient, links, clicked_at = timestamp1
| where isempty(clicked_at)
```
<br>

**Answer: 0**<br><br>

**Q6. How many employees received an email but did not click on the attached link?**<br><br>

```
Email
| where links has "api-sync-updates.top"
| mv-expand links to typeof(string)
| join kind=leftouter Employees on $left.recipient == $right.email_addr
| join kind=leftouter (    
    ProxyEvents
    | where url has "api-sync-updates.top"
) on $left.ip_addr == $right.src_ip, $left.links == $right.url
| project timestamp, sender, recipient, links, clicked_at = timestamp1
```
<br>

**Answer: 2**<br><br>

**Q7. Click Next to Continue**<br><br>

**Q8. Enter anti join to continue.**<br><br>

**Answer: anti join**<br><br>


**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
