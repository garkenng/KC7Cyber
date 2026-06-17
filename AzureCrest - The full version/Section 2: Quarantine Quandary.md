## AzureCrest - The full version: Section 2: Quarantine Quandary<br>
### **Summary**<br>
We received a security alert a few days ago that a file with the word 'healthcare' was quarantined. We know that it's your first day here, but we get these alerts all the time and they are usually nothing. What could possibly go wrong?
<br><br>

**Q1. What is the name of the file that was quarantined?**<br><br>

```
SecurityAlerts
| where description contains "healthcare"
```
<br>

First result, under the column indictor:<br><br>

```
[{'hostname': 'ZQHM-LAPTOP', 'filename': 'New_Healthcare_Protocols.docm', 'sha256': '9195246412dc64c15e429887cac945bbde13c249d25dad01c7245219d1ac021a'}]
```
<br>

**Answer: New_Healthcare_Protocols.docm**<br><br>

**Q2. What is the hostname of the computer that contained this file?**<br><br>
From previous query.<br><br>

**Answer: ZQHM-LAPTOP**<br><br>

**Q3. What is the name of the employee that this computer belongs to?**<br><br>

```
Employees
| where hostname == "ZQHM-LAPTOP"
```
<br>

**Answer: Jerry Jones**<br><br>

**Q4. What is that employee's role at Azure Crest Hospital?**<br><br>
From previous query.<br><br>

**Answer: Resident Doctors**<br><br>

**Q5. When was this file created on the doctor's computer? (paste the full timestamp)**<br><br>

```
FileCreationEvents
| where filename == "New_Healthcare_Protocols.docm"
| where hostname == "ZQHM-LAPTOP"
```
<br>

**Answer: 3/14/2024, 10:38:36 AM**<br><br>

**Q6. What process did we see create this file? (process name)**<br><br>
From previous query.<br><br>

**Answer: chrome.exe**<br><br>

**Q7. What domain was the file downloaded from?**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.174"
| where url contains "New_Healthcare_Protocols.docm"
```
<br>

**Answer:  takeyatimecarepartners.com**<br><br>

**Q8. Which legitimate Azure Crest partner's domain is the threat actor attempting to mimic?**<br><br>
From the training guide on website, there is a reference to emergencycarepartners.com. This address is similar to takeyatimecarepartners.com as discovered in question 7.<br><br>

**Answer:  emergencycarepartners.com**<br><br>

**Q9. What is Jerry's email address?**<br><br>

```
Employees
| where name contains "Jerry"
```
<br>

**Answer: jerry_jones@azurecresthospital.med**<br><br>

**Q10. How many emails did Jerry Jones receive?**<br><br>

```
Email
| where recipient == "jerry_jones@azurecresthospital.med"
```
<br>

**Answer: 23**<br><br>

**Q11. When did Jerry receive the email that contained a link to the quarantined file? (paste the full timestamp)**<br><br>

```
Email
| where recipient == "jerry_jones@azurecresthospital.med"
| where link contains "New_Healthcare_Protocols.docm"
```
<br>

**Answer: 3/14/2024, 10:27:39 AM**<br><br>

**Q12. What is the sender's address for that email?**<br><br>
From previous query.<br><br>

**Answer: medstaffinfo@hospitalcomm.org**<br><br>

**Q13. What 'reply to' address is used?**<br><br>
From question 11.<br><br>

**Answer: healthupdate@gmail.com**<br><br>

**Q14. What is the subject of the email?**<br><br>
From question 11.<br><br>

**Answer: [EXTERNAL] FW: 🚑 Attention Required: Urgent Pediatric Health Procedure Update 🌈**<br><br>

**Q15. When did Jerry receive that email? (paste the full timestamp)**<br><br>

```
Email
| where recipient == "jerry_jones@azurecresthospital.med"
| where sender == "healthupdate@gmail.com"
```
<br>

**Answer: 3/6/2024, 11:49:48 AM**<br><br>

**Q16. What is filename seen in the link?**<br><br>
From previous query, under link column.<br><br>

**Answer: Pediatric_Care_Update.docm**<br><br>

**Q17. Type RIP to receive credit.**<br><br>

**Answer: RIP**<br><br>

