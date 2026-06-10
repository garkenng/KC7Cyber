## Inside Encryptodera: An Insider Threat Scenario: 1: Offensive Odor<br>
### **Summary**<br>
Now, we're getting started with the investigation!
<br><br>
A few employees have reported that Barry Shmelly has been behaving strangely. One employee showed you this tweet from Barry.
<br><br>
Normally Barry is a very cool, calm, and collected cat. But lately, here's been more of a snapping tiger. It might have something to do with the layoff rumors.
<br><br>

**Q1. What is Barry's role at the company?**<br><br>

```
Employees
| where name contains "Barry"
```
<br>

**Answer: StackOverflow Copy Paster**<br><br>

**Q2. What is Barry's email address?**<br><br>
From previous query

**Answer: barry_shmelly@encryptoderafinancial.com**<br><br>

**Q3. What was the subject of the interesting email (the one on January 16th) that Barry sent?**<br><br>

```
Email
| where sender == "barry_shmelly@encryptoderafinancial.com"
| where timestamp >= datetime(01/16/2024)
```
<br>

**Answer: I'm not coming in today. I'm sick of this place. We're all getting laid off anyway.**<br><br>


**Q4. What was the role of the employees that received Barry's email?**<br><br>
Using the first email address from the previous query, run search for that employee to find their role.<br><br>

```
Employees
| where email_addr == "christopher_naylor@encryptoderafinancial.com"
```
<br>

**Answer: Social Media Manager**<br><br>


**Q5. On January 18, Barry sent an email with the subject "YOU ARE A GREEDY PIG!!!! WHAT IS WRONG WITH YOU?????" What was the role of the recipient of that email?**<br><br>

```
let EmailRole = Email
| where sender == "barry_shmelly@encryptoderafinancial.com"
| where timestamp >= datetime(01/18/2024)
| where subject contains "YOU ARE A GREEDY PIG!!!! WHAT IS WRONG WITH YOU?????"
| distinct recipient;
Employees
| where email_addr in (EmailRole)
| project role
```
<br>

**Answer: Chief Executive Officer**<br><br>

**Q6. What's Barry's IP address? (Paste the full IP address )**<br><br>

```
Employees
| where name contains "Barry"
```
<br>

**Answer: 10.10.0.1**<br><br>

**Q7. What was the complete URL that Barry was browsing on his computer regarding Cybersecurity Insiders on the afternoon of December 26th?(Paste the full url)**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.1"
| where timestamp >= datetime(12/01/2023)
| where url contains "Cybersecurity"
```
<br>

**Answer: https://www.cybersecurity-insiders.com/safe-ways-to-transfer-sensitive-files**<br><br>

**Q8. What website did he visit first on January 15th? (Paste the full URL)**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.1"
| where timestamp >= datetime(1/15/2024)
```
<br>

**Answer: https://www.7-zip.org/a/7z2002-x64.exe**<br><br>

**Q9. Could you provide the full URL for the website Barry searched for USB Flash Drives?**<br><br>
From previous query.<br><br>

**Answer: https://www.wikihow.com/Use-a-USB-Flash-Drive**<br><br>

**Q10. What "secret" document on business transactions did Barry download?**<br><br>

```
InboundNetworkEvents
| where src_ip == "10.10.0.1"
| where timestamp >= datetime(1/15/2024)
| where url contains "secret"
```
<br>

**Answer: SECRET_MergersAndAcquisitions_Strategy2025.docx**<br><br>

**Q11. What document (docx) did Barry download about salaries?**<br><br>
Using the previous query.<br><br>

**Answer: ExecutiveSalaryNegotiations.docx**<br><br>

**Q12. What document (zip) did Barry download to get this?**<br><br>

```
ProcessEvents
| where hostname == "IGOY-DESKTOP"
| where timestamp >= datetime(1/15/2024)
| where process_commandline contains "zip"
```
<br>

**Answer: Encryptodera_Proprietary_Algorithms.zip**<br><br>

**Q13. Do you know the password he used to zip the files?**<br><br>

```
ProcessEvents
| where hostname == "IGOY-DESKTOP"
| where timestamp >= datetime(1/16/2024)
| where process_commandline contains "-p"
```
<br>
Taking the first result.<br><br>

```
7z.exe a -t7z C:\Users\bashmelly\Documents\To_Take\Company_Secrets.7z C:\Users\bashmelly\Documents\To_Take\*.docx -p securePass123
```
<br>

**Answer: securePass123**<br><br>

**Q14. What is the name of the drive on which Barry stored the final files?**<br><br>

```
ProcessEvents
| where process_commandline has "Encryptodera_Proprietary_Algorithms.zip"
```
<br>

**Answer: SchmellyDrive**<br><br>

**Q15. Type gotheem to take credit**<br><br>

**Answer: gotheem**<br><br>
