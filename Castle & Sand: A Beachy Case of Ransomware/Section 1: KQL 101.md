## Castle & Sand: A Beachy Case of Ransomware: Section 1: KQL 101<br>
### **Summary**<br>
<p>
Castle&Sand is a leading beach gear company with stores across many locations. Known for high-quality, innovative products and expert staff, it offers a top-tier shopping experience. Its focus on customer satisfaction, trend-setting design, and welcoming stores makes it a trusted destination for beachgoers.

🥳 Today is your first day as a Junior Security Operations Center (SOC) Analyst with our company. Your primary job responsibility is to defend Castle&Sand and our employees from malicious cyber actors.

Remember The training guide will teach you how to answer the KQL101 questions.

Let's get started with a KQL 101. You can skip it if you've done this before.

The Employees table contains information about all the employees in our organization. In this case, we can see that the organization is named “Castle&Sand” and the domain is “castleandsand.com”.

Do a take 10 on all the other tables to see what kind of data they contain.
</p>

**Q1. Type done here when finished to earn your first 10 points!**<br><br>

**Answer: done**<br><br>

**Q2. How many employees are in the company?**<br><br>

```
Employees
| count
```
<br>

**Answer: 1500**<br><br>

**Q3. Which employee has the IP address: 10.10.2.1?**<br><br>

```
Employees
| where ip_addr == "10.10.2.1"
```
<br>

**Answer: Preston Lane**<br><br>

**Q4. How many emails did Jacqueline Henderson receive?**<br><br>

<p>
Need to look for Jacqueline Henderson email address first.
</p>

```
Employees
| where name contains "Jacqueline Henderson"
```
<br>

<p>
  Use the email address in the email table.
</p>

```
Email
| where recipient == "jacqueline_henderson@castleandsand.com"
| count
```
<br>

**Answer: 26**<br><br>

**Q5. How many distinct senders were seen in the email logs from sunandsandtrading.com?**<br><br>

```
Email
| where sender has "sunandsandtrading.com"
| distinct sender
| count
```
<br>

**Answer: 2146**<br><br>

**Q6. How many unique websites did “Cristin Genao” visit?**<br><br>

**Answer: **<br><br>

**Q7. **<br><br>

**Answer: **<br><br>

**Q8. **<br><br>

**Answer: **<br><br>

**Q9. **<br><br>

**Answer: **<br><br>



