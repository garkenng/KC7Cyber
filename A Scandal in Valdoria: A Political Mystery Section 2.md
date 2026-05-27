## A Scandal in Valdoria: A Political Mystery<br>
### **Section 2**<br>

**Q1 What is the Newspaper Printer's name?**<br><br>
Based on the conversation via text on the website, the printers name is Clark Kent.<br><br>
**Answer: Clark Kent**

**Q2 What is the Editorial Intern's name?**<br><br>
From the Employees table, can retrieve the interns name by searching for the role 'Editorial Intern'.<br><br>

```
Employees
| where role has "Editorial Intern"
```
<br>

**Answer: Ronnie McLovin**<br><br>

**Q3 When was the Editorial Intern hired at The Valdorian Times?**<br><br>
From the previous query, we can find the hired date.<br><br>
**Answer: 1/2/2024, 8:00:00 AM**<br><br>

**Q4 How many total emails has Clark Kent received?**<br><br>
