## A Rap Beef: An Intro to Security Investigations: Less Beef More Phish<br>
### **Summary**<br>
The higher ups at OWL records deliberated the happening in a private meeting. In that meeting was Dwake himself who was seething about what had taken place.
<br><br>
After 6 hours of deliberation, the company declared it a settled issue. However, they never officially specified how they dealt with the situation.
<br><br>
The following day, a random hacker on the dark web threatened to release damaging information on Present the rapper, if he did not announce his retirement in the next 30 days.<br><br>
**Q1 Enter darkweb to continue**<br><br>

**Answer: darkweb**<br><br>

**Q2 Type lesdoit to continue**<br><br>

**Answer: lesdoit**<br><br>

**Q3 What domain did IP 18.66.52.227 resolve to?**<br><br>
Looking in the Passive DNS table, can view what domains the IP address resolves to.<br><br>

```
PassiveDns
| where ip == "18.66.52.227"
```
<br>

**Answer: betterlyrics4u.com**<br><br>

**Q4 Which column in the email table is most likely to contain our domain?**<br><br>
Can use the take command in the Email table to list the columns the table has.<br><br>

```
Email
| take 10
```
<br>

**Answer: link**<br><br>

**Q5 How many results did we get from this query?**<br><br>
A KQL query has been given, need to run it to see how many results it returns<br><br>

```
Email
| where link has "betterlyrics4u.com"
```
<br>

**Answer: 13**<br><br>

**Q6 Which email address was used to send most of these emails?**<br><br>
Answer shown from previous question query.<br><br>

**Answer: ghostwritersanonymous@protonmail.com**<br><br>

**Q7 What was the other email address used to send these phishing emails?**<br><br>
The other email address listed from question 5 in the results is wemakebeatz@gmail.com.<br><br>

**Answer: wemakebeatz@gmail.com**<br><br>

**Q8 Which role was targeted the most of all?**<br><br>
A KQL query is given, run the query to get which role was targeted the most.<br><br>

```
let _targets = Email
| where link has "betterlyrics4u.com"
| distinct recipient;
Employees
| where email_addr in (_targets)
```
<br>

**Answer: Rapper**<br><br>

**Q9 Which role (other than Rapper) was targeted by this phishing campaign?**<br><br>
There is another role shown in the results from previous question query.<br><br? 

**Answer: Lead Rapper**<br><br>
