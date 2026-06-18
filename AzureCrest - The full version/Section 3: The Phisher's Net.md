## AzureCrest - The full version: Section 3: Derpy Database<br>
### **Summary**<br>
In the previous section, we identified a series of suspicious files with a healthcare theme. Let's widen our investigation to see if other employees were targeted with these suspicious files.





**Q1. How many Azure Crest employees received emails containing a link to the previously identified (.docm) files?**<br><br>

```
Email
| where link contains ".docm"
| distinct recipient
```
<br>

**Answer: 40**<br><br>

**Q2. How many distinct subjects did the threat actors use in this batch of emails?**<br><br>
Need to filter out any forwarded emails.<br><br>

```
Email
| where link contains ".docm"
| where subject !contains "FW:"
| distinct subject
```
<br>

**Answer: 7**<br><br>

**Q3. How many distinct links did the threat actors use in this batch of emails?**<br><br>

```
Email
| where link contains ".docm"
| distinct link
```
<br>

**Answer: 17**<br><br>


**Q4. How many distinct domains were used in this batch of emails?**<br><br>

```
Email
| where link contains ".docm"
| extend domain = parse_url(link).Host
| distinct tostring(domain)
```
<br>

**Answer: 4**<br><br>



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

