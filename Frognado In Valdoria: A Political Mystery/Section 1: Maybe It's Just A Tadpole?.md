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


**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
**Q2. **<br>

**Answer: **<br><br>
