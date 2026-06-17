## AzureCrest - The full version: Section 4: Quarantine Quandary<br>
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
