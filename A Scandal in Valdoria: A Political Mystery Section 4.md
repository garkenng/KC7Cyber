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
Using query from question 2, the subject line can be pulled from the column subject.<br><br>

**Answer: [EXTERNAL] Breaking News: We're Hiring! Apply Now for Reporter Roles**<br><br>


**Q5 When did Ronnie click on the link in the email from valdorias_best_recruiter@gmail.com ?**<br><br>
Search for the domain in the Outboundnetwork table. <br><br>

```
OutboundNetworkEvents
| where url has "promotionrecruit.org"
```
<br>

The first result shows when the link was clicked. Can cross reference this with the source IP address of 10.10.0.19, which is Ronnies user account.<br><br>

**Answer: 1/10/2024, 8:55:07 AM**<br><br>

**Q6 What was the name of the .docx file that was downloaded to Ronnie's machine?**<br><br>
From the query in question 5, the url for the first entry has the name of the docx file.<br>

**Answer: Editorial_J0b_Openings_2024.docx**<br><br>

**Q7 When was this docx file downloaded?**<br><br>
