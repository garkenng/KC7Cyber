## Inside Encryptodera: An Insider Threat Scenario: 3: F In The Chat<br>

**Q1. Wipe away your tears. It's time to figure out how the threat actor compromised the domain controller. What username was used to log into the DOMAIN_CONTROLLER_SERVER?**<br><br>

```
AuthenticationEvents
| where hostname == "DOMAIN_CONTROLLER_SERVER"
```
<br>

**Answer: lihenry_domain_adminready**<br><br>

**Q2. What laptop did the lihenry_domain_admin account sign into? (Enter the hostname)**<br><br>

```
AuthenticationEvents
| where username == "lihenry_domain_admin"
```
<br>

**Answer: GJ95-LAPTOP**<br><br>

**Q3. What is the MITRE ATT&CK ID for mimikatz?**<br><br>
Run a Google search for the ID.<br><br>

**Answer: S0002**<br><br>


**Q4. Let's check to see if the threat actor ran mimikatz on GJ95-LAPTOP. Did the threat actor run mimikatz on this device? If so, enter the command line the attacker ran. If not, enter no.**<br><br>

```
ProcessEvents
| where hostname == "GJ95-LAPTOP"
| where process_commandline contains "mimikatz"
```
<br>

**Answer: totally_not_mimikatz.exe "sekurlsa::logonpasswords"**<br><br>

**Q5. Who does this device belong to? (Enter the employee's name)**<br><br>

```
Employees
| where hostname == "GJ95-LAPTOP"
```
<br>

**Answer: Valerie Orozco**<br><br>


**Q6. Was Valerie Orozco targeted in the phishing emails sent from Barry Shmelly?**<br><br>

```
Email
| where sender == "barry_shmelly@encryptoderafinancial.com"
| where timestamp >= datetime(01/02/2024)
| where link contains "update"
| where recipient == "valerie_orozco@encryptoderafinancial.co
```
<br>

One result is returned.<br><br>

**Answer: yes**<br><br>

**Q7. What is the name of the file that was sent to Valerie in the phishing email?**<br><br>
From previous query.<br><br>

**Answer: Employee_Contact_List_Updated_March_2024.docx.exe**<br><br>

**Q8. Did Valerie click the link? If so, enter the timestamp when she clicked the link. If not, enter 'no'**<br><br>
```
OutboundNetworkEvents
| where src_ip == "10.10.0.18"
| where url contains "http://update-finance-security.biz/public/images/files/Employee_Contact_List_Updated_March_2024.docx.exe"
```
<br>
No results are returned.<br><br>

**Answer: No**<br><br>

**Q9. How many different user accounts logged into Valerie's machine?**<br><br>

```
AuthenticationEvents
| where hostname == "GJ95-LAPTOP"
| distinct username
```
<br>

**Answer: 3**<br><br>

**Q10. How many unique hosts did this user account attempt to log into?**<br><br>

```
AuthenticationEvents
| where username == "systadmi_local_admin"
| distinct hostname
| count
```
<br>

**Answer: 10**<br><br>

**Q11. **<br><br>
**Answer: **<br><br>

**Q11. Which user NOT in an IT role was improperly using the systadmi_local_admin credentials? (This is likely a sign of compromise)**<br><br>

```
let hosts = FileCreationEvents
| where filename has "screenconnect"
| distinct hostname;
AuthenticationEvents
| where hostname in (hosts)
| where username has "systadmi"
| where result has "Successful"
| join (
    Employees 
    | project ip_addr,role,email_addr,name
) on $left.src_ip==$right.ip_addr
| project SourceIpName=name, a="who is a", SourceIpUserRole=role, b="logged onto",hostname, c="using", username, d="at",timestamp
```
<br>

**Answer: Robin Kirby**<br><br>

**Q12. When was Robin phished by Barry Shmelly's account?**<br><br>

```
Email
| where recipient == "robin_kirby@encryptoderafinancial.com"
| where sender == "barry_shmelly@encryptoderafinancial.com"
```
<br>

**Answer: 2/1/2024, 3:59:30 AM**<br><br>

**Q13. Type letsgo to move on!**<br><br>
**Answer: letsgo**<br><br>

**Q14. **<br><br>
**Answer: **<br><br>

**Q15. **<br><br>
