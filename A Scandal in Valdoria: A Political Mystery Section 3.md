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

```
FileCreationEvents
| where hostname has "UL0M-MACHINE" and path contains "Valdorian_Times_Editorial_Offer_Letter.docx"
```
<br>

**Answer: 1/5/2024, 10:24:04 AM**<br><br>

**Q10 What was the full path of the docx file that was downloaded to Sonia's machine?**<br><br>
Using the query from the previous question, the full path of the docx can be found. <br><br>

**Answer: C:\Users\sogose\Downloads\Valdorian_Times_Editorial_Offer_Letter.docx**<br><br>

**Q11 What is the sha256 hash of the file that Sonia downloaded?**<br><br>
Using the query from question 9, the sha256 can be found.

**Answer: 60b854332e393a6a2f0015383969c3ac705126a6b7829b762057a3994967a61f**<br><br>

**Q12 What is the name of the file (.ps1) that was written to disk immediately after the docx was downloaded?**<br><br>

Search for files that were created right after the file was downloaded at 01/05/2024 10:24:04 along with the hostname of UL0M-MACHINE.<br><br>

```
FileCreationEvents
| where timestamp > datetime(01/05/2024 10:24:04) and hostname contains "UL0M-MACHINE"
```
<br>

The first result that comes back was recorded at 1/5/2024, 10:24:32 AM, 28 seconds after the file was downloaded. This is likely the file that was created under the path column.

**Answer: hacktivist_manifesto.ps1**<br><br>

**Q13 When was this new file created?**<br><br>

From the previous query it shows in the timestamp when the file was created.<br><br>

**Answer: 1/5/2024, 10:24:32 AM**<br><br>

**Q14 Let's do some research! What type of file is this?**<br><br>

Using google, the file extension ps1 is a powershell script.

**Answer: Powershell**<br><br>
