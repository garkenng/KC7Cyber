## AzureCrest - The full version: Section 3: Derpy Database<br>
### **Summary**<br>
In the previous section, we identified a series of suspicious files with a healthcare theme. Let's widen our investigation to see if other employees were targeted with these suspicious files.





**Q1. How many Azure Crest employees received emails containing a link to the previously identified (.docm) files?**<br><br>

```
Email
| where link contains ".docm"
| distinct recipient
```
<br>

**Answer: 40**<br><br>

**Q2. How many distinct subjects did the threat actors use in this batch of emails?**<br><br>
Need to filter out any forwarded emails.<br><br>

```
Email
| where link contains ".docm"
| where subject !contains "FW:"
| distinct subject
```
<br>

**Answer: 7**<br><br>

**Q3. How many distinct links did the threat actors use in this batch of emails?**<br><br>

```
Email
| where link contains ".docm"
| distinct link
```
<br>

**Answer: 17**<br><br>


**Q4. How many distinct domains were used in this batch of emails?**<br><br>

```
Email
| where link contains ".docm"
| extend domain = parse_url(link).Host
| distinct tostring(domain)
```
<br>

**Answer: 4**<br><br>



**Q5. How many employees clicked on the email links?**<br><br>

```
let ClickedOnLinks = 
    Email
    | where link contains "Pediatric_Care_Update.docm" or link contains  "New_Healthcare_Protocols.docm" 
    | where sender == "medstaffinfo@hospitalcomm.org" or sender == "healthupdate@gmail.com"
    | distinct link;
    OutboundNetworkEvents
    | where url in (ClickedOnLinks)
    | distinct src_ip
    | count
```
<br>

**Answer: 37**<br><br>

**Q6. How many records are there for either of these files being on Azure Crest employee computers?**<br><br>

```
FileCreationEvents
| where filename contains "Pediatric_Care_Update.docm" or filename contains  "New_Healthcare_Protocols.docm"
```
<br>

**Answer: 38**<br><br>

**Q7. What is the timestamp for the first time one of these files was created?**<br><br>
From previous query.<br><br>

**Answer: 3/1/2024, 11:58:33 AM**<br><br>

**Q8. What is the name of the file that is created after the suspicious file is downloaded?*<br><br>

```
FileCreationEvents
| where hostname == "P3EX-DESKTOP"
| where timestamp > datetime(3/1/2024, 11:58:33 AM)
```
<br>

**Answer: heartburn.zip**<br><br>

**Q9. What is the directory path that contains this new file?**<br><br>
From previous query.<br><br>

**Answer: C:\ProgramData\Heartburn\heartburn.zip**<br><br>

**Q10. On that machine, how many additional files are created in the same directory?**<br><br>
3 additional files were created after the heartburn.zip.<br><br>

```
C:\ProgramData\Heartburn\anydesk.exe
C:\ProgramData\Heartburn\putty.exe
C:\ProgramData\Heartburn\secretsdump.exe
```
<br>

**Answer: 3**<br><br>

**Q11. What command was used to extract the additional files from the zip file into the same directory where it was located?**<br><br>

```
ProcessEvents
| where process_commandline contains "heartburn.zip"
| where process_name == "cmd.exe"
```
<br>

**Answer: cmd.exe /c Expand-Archive -Path C: \ProgramData\heartburn.zip -DestinationPath C:\ProgramData\Heartburn**<br><br>

**Q12. What is the IP address that putty.exe uses to establish it's SSH connection?**<br><br>


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
**Q.**<br><br>


**Answer: **<br><br>

