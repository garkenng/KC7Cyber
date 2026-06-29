## Cowboy Couture: A Steampunk Space Adventure: Section 3: Cyber Cattle Thief<br>
### Summary
Well partner, it looks like you're ready to help us solve this cyber mystery! 🕵️‍♀️
<br><br>
Celestial Cowboy Couture has spent months planning and pouring money into launching their most anticipated collection. They even hired a superstar fashion CEO to take them to the next level and stand alongside the big French and Italian brands. Everything was set for the big launch, but just as they were ready to unveil the collection, an employee noticed something disturbing: some of their designs had already been knocked off and were available on OutlawBuy.com! 😱
<br><br>

**Q1. Enter Oh no to continue.**<br>

**Answer: Oh no**<br><br>

**Q2. Enter Saddle up to continue.**<br>

**Answer: Saddle up**<br><br>

**Q3. What is the name of the Lead Fashion Designer?**<br>

```
Employees
| where role == "Lead Fashion Designer"
```
<br>

**Answer: Megan Lucia**<br><br>

**Q4. Does it look like Megan was up to suspicious activity that needs to be investigated further? (Yes/No)**<br>

```
FileCreationEvents
| where hostname == "ITCK-MACHINE"
| order by timestamp desc
```
<br>

Browsing through the results, there are a number of entries with the folder titled 'designs_to_steal'.
<br><br>

```
C:\Users\melucia\Documents\designs_to_steal\2025_cowboy_vanity_fair_designs_SO_CHIC.zip
```
<br>

**Answer: Yes**<br><br>


**Q5. How many of these zip files were created on Megan's machine?**<br>

```
FileCreationEvents
| where hostname == "ITCK-MACHINE"
| where path contains ".zip"
| order by timestamp desc
```
<br>

**Answer: 4**<br><br>


**Q6. What folder were the zip files placed in on Megan's machine?**<br>
From previous query.<br><br>

**Answer: designs_to_steal**<br><br>

**Q7. An executable file, advanced-uploader.exe, appears on Megan’s machine after the creation of the zip files. What is the timestamp for when this file was created?**<br>

```
FileCreationEvents
| where hostname == "ITCK-MACHINE"
| where path contains "advanced-uploader.exe"
```
<br>

**Answer: 10/2/2024, 8:36:47 AM**<br><br>

**Q8. Was this process executed on Megan's machine?(Yes/No)**<br>

```
ProcessEvents
| where hostname == "ITCK-MACHINE"
| where process_name == "advanced-uploader.exe"
```
<br>
If a result is returned, then the process was executed on Megan's machine.<br><br>

**Answer: Yes**<br><br>


**Q9. What is the full URL where the files were exfiltrated to?**<br>

**Answer: **<br><br>
**Q.**<br>

**Answer: **<br><br>
**Q.**<br>

**Answer: **<br><br>
**Q.**<br>

**Answer: **<br><br>
