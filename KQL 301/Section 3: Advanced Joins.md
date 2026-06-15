## KQL 301: Section 3: Advance Joins<br>

**Q1. Click Submit to continue**<br><br>

**Answer: join the hunt**<br><br>


**Q2. How many results do we get back after the join?**<br><br>

```
Email
| where sender == "diego_hernandez@whiskersandwonders.org"
| join kind=leftouter Employees on $left.recipient == $right.email_addr
| project-reorder timestamp, sender, recipient, ip_addr
```
<br>

**Answer: 15**<br><br>

**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
