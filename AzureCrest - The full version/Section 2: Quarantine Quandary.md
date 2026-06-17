## AzureCrest - The full version: Section 2: Quarantine Quandary<br>
### **Section 2**<br>
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

**Answer: **<br><br>

**Q8.**<br><br>

**Answer: **<br><br>

**Q9.**<br><br>

**Answer: **<br><br>

**Q10.**<br><br>

**Answer: **<br><br>

**Q11.**<br><br>

**Answer: **<br><br>

**Q12.**<br><br>

**Answer: **<br><br>

**Q13.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

