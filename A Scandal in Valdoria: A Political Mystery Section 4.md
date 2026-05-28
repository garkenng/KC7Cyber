## A Scandal in Valdoria: A Political Mystery<br>
### **Section 4**<br>
### **Summary**<br>
We can apply what we've learned by investigating the activity affecting Sonia to find other victims of this incident.
<br><br>
I hope you took good notes. Another suspicious email address valdorias_best_recruiter@gmail.com was seen sending emails to intern Ronnie and a few others.
<br><br>
**Q1 How many total emails were sent by this email sender to users at The Valdorian Times?**<br><br>

```
Email
| where sender == "valdorias_best_recruiter@gmail.com"
| count
```
<br>

**Answer: 18**<br><br>

**Q2 When did valdorias_best_recruiter@gmail.com send an email to Ronnie McLovin?**<br><br>

Can use the from and to email address in next query to find the timestamp.

```
Email
| where sender == "valdorias_best_recruiter@gmail.com"
| where recipient == "ronnie_mclovin@valdoriantimes.news"
```
<br>

**Answer: 1/10/2024, 8:48:16 AM**<br>

**Q3 What domain was in the link from that email?**<br><br>
From the previous query, the domain can be pulled from the link column. <br><br>

**Answer: promotionrecruit.org**<br><br>

**Q4 What was the subject of that email?**<br><br>
