## A Scandal in Valdoria: A Political Mystery<br>
### **Section 3**<br>
### **Summary**<br>
You stop by The Valdorian Times office and meet with some staff. After the meeting, one employee, Sonia Gose, comes up to you and says she may have something that can help with your investigation.<br><br>

**Q1 What is Sonia's job role?**<br><br>

```
Employees
| where name contains "Sonia"
```
<br>

**Answer: Senior Editor**<br><br>

From ther website 'Sonia shows you a suspicious email she received a few weeks ago.'<br><br>

**Q2 What email address was used to send this email?**<br><br>

Referring to the picture of an email on the website. The email addresa can be seen on the first line.<br><br>

**Answer: newspaper_jobs@gmail.com**<br><br>

**Q3 When was the email sent to Sonia Gose? Enter the exact timestamp from the logs.**<br><br>

We know the sender and receipient email address. Can combine these two into a single query.<br><br>

```
Email
| where recipient has "sonia_gose@valdoriantimes.news" and sender has "newspaper_jobs@gmail.com"
```
<br>

**Answer: 2024-01-05T09:42:05Z**<br><br>

**Q4 What URL was included in the email?**<br><br>
Using the query from question 3.<br><br>

**Answer: https://promotionrecruit.com/published/Valdorian_Times_Editorial_Offer_Letter.docx**<br><br>

**Q5 What is Sonia Gose's IP address?**<br><br>
Pull the IP address from the Employees table.

```
Employees
| where name contains "Sonia"
```
<br>


**Answer: 10.10.0.3**<br><br>

**Q6 Did Sonia click on this link? If so, enter the timestamp when she clicked the link. If not, type "no".**<br><br>

```
OutboundNetworkEvents
| where url has "https://promotionrecruit.com/published/Valdorian_Times_Editorial_Offer_Letter.docx" and src_ip has "10.10.0.3"
```
<br>

**Answer: 1/5/2024, 10:23:17 AM**<br><br>

**Q7 What was the name of the docx file in the link that Sonia clicked?**<br><br>

Using the previous query, can pull the name of the docx file that was clicked under the url column.<br><br>

**Answer: Valdorian_Times_Editorial_Offer_Letter.docx**<br><br>

**Q8 What is Sonia Gose's hostname?**<br><br>

Using the query from question 1, the hostname can be pulled from the Employees table.<br><br>

**Answer: UL0M-MACHINE**<br><br>

**Q9 When did the downloaded docx file first show up on Sonia's machine?**<br><br>
