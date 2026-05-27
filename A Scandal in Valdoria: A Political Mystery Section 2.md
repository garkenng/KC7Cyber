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
Retrieve Clark Kent email from the Employees table.<br><br>

```
Employees
| where name contains "Clark"
```
<br>
Clark Kent email address is: clark_kent@valdoriantimes.news.
<br><br>

```
Email
| where recipient has "clark_kent@valdoriantimes.news"
| count
```
<br>

**Answer: 21**<br>

From the website 'Review the emails sent to Clark Kent for the one sent on January 31, 2024 containing the final edits for the election OpEd.'

**Q5 What was the subject line of this email?**<br><br>
Search for the date and receipient to narrow the results down.<br><br>

```
Email
| where timestamp between (startofday(datetime(2024-01-31)) .. endofday(datetime(2024-02-01))) and  recipient has "clark_kent@valdoriantimes.news"
```
<br>
One result is returned.
<br><br>
**Answer: URGENT: Final OpEd Draft Edits (Please publish the following article in tomorrow's paper))**<br><br>

