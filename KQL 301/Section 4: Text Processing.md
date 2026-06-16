## KQL 301: Section 4: Text Processing<br>

**Q1. How many characters are in the longest email address username?**<br><br>

```
Employees
| parse email_addr with username "@" *
| project username, UserNameLength = strlen(username)
```
<br>

**Answer: 17**<br><br>

**Q2. What is the first filename created on pawilson's machine?**<br><br>

**Answer: **<br><br>


**Q3. **<br><br>

**Answer: **<br><br>


**Q4. **<br><br>

**Answer: **<br><br>

