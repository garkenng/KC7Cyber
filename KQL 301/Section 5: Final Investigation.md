## KQL 301: Section 5: Final Investigation<br>
### **Summary**<br>
Time to put it all together.
<br><br>
You've learned:
<br><br>
let + in for filtering across tables
lookup for enrichment
join types: inner, leftouter, leftanti, leftsemi
union for searching across tables
mv-expand for array handling
parse and split for text extraction
Now trace the complete attack chain.
<br><br>

**Q1. Enter final challenge to continue.**<br><br>

**Answer: final challenge**<br><br>


**Q2. Challenge 1: Identify all phishing recipients. Find all employees who received the phishing email from noreply@whiskersandwonders-hr.com with their names and roles.How many unique employees received the phishing email?**<br><br>

```
let PhisingEmail = 
    Email
    | where sender == "noreply@whiskersandwonders-hr.com"
    | distinct recipient;
Employees
| where email_addr in (PhisingEmail)
```
<br>

**Answer: 3**<br><br>

**Q1. **<br><br>

**Answer: **<br><br>


**Q1. **<br><br>

**Answer: **<br><br>
**Q1. **<br><br>

**Answer: **<br><br>
**Q1. **<br><br>

**Answer: **<br><br>
**Q1. **<br><br>

**Answer: **<br><br>
**Q1. **<br><br>

**Answer: **<br><br>
