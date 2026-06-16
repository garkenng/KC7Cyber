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

**Q3. Challenge 2: Calculate click rate. Join phishing emails with click events to find who clicked. What percentage of emails resulted in a click? (Round to nearest whole number)**<br><br>

**Answer: 33%**<br><br>





**Q4. Challenge 3: Confirm active compromise. Find evidence of ongoing C2 communication from compromised workstations. How many accounts appear to be compromised?**<br><br>

**Answer: **<br><br>


**Q5. Challenge 4: Find most recent attacker activity. Identify the latest C2 communication. What is this type of activity called?**<br><br>

**Answer: **<br><br>

**Q6. Challenge 5: Calculate attack duration. Use union to build a complete timeline from first phishing email to last C2 beacon. How many minutes passed between the first phishing email and the attacker's last action?**<br><br>

**Answer: **<br><br>

**Q7. Enter level 301 complete to finish**<br><br>

**Answer: level 301 complete**<br><br>

