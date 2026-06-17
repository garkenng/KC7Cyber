## Frognado In Valdoria: A Political Mystery: Section 4: Nope, It's A Full on Frognado!!!!<br>
### **Summary**<br>
You look above the screen of your computer, checking that the creepy guy is nowhere to be seen. He’s not. Phew. You get up and run to the break room to get a cup of coffee. While the machine brews your beverage, you go over what you’ve found so far.
<br><br>
Three employees have been targeted in a seemingly internal spearphishing attack. Those attacks were successful and allowed the Shadow Truth to deface FramtidX’s website and ruin their architectural plans. Also frogs. That was the easy part.
<br><br>
The coffee machine bips. You grab your cup and walk back to your desk, pondering your next steps. You think you should investigate Alex Johnson. That employee was the source of the phishing emails. They might have been compromised themselves, or they could be an insider threat. Either way, investigating them will allow you to confirm and/or find out the entry point for the attack, but also verify if anybody else was targeted.
<br><br>
You take a sip of your coffee and start to type a new query.
<br><br>


**Q1. What is Alex Johnson’s role in the company?**<br><br>

```
Employees
| where name == "Alex Johnson"
```
<br>

**Answer: Developer**<br><br>


**Q2. How many internal phishing emails were sent from Alex’s email address?**<br><br>
Use the Phising domains from previous sections.<br><br>

```
Email
| where sender == "alex_johnson@framtidxdevcorp.com"
| where link contains "newdevelopmentupdates.org" or link contains  "greenprojectnews.net"
```
<br>

**Answer: 7**<br><br>

**Q3. How many distinct roles were targeted by the spearphishing emails?**<br><br>

```
let DistinctRoles = 
    Email
    | where sender == "alex_johnson@framtidxdevcorp.com"
    | where link contains "newdevelopmentupdates.org" or link contains  "greenprojectnews.net"
    | distinct recipient;
Employees
| where email_addr in (DistinctRoles)
| distinct role
```
<br>


**Answer: 4**<br><br>


**Q4. What is the name of the very important person who was targeted?**<br><br>
Previous query showed role of CEO.<br><br>

```
Employees
| where role == "CEO"
```
<br>

**Answer: Johanna Karlsson**<br><br>


**Q5. What was the subject of the mail targeting the person found in Q4?**<br><br>

```
Email
| where sender == "alex_johnson@framtidxdevcorp.com"
| where recipient == "johanna_karlsson@framtidxdevcorp.com"
```
<br>

**Answer: Urgent: Security Update Required**<br><br>

**Q6. What are they trying to find out about the person from Q4?**<br><br>

```
InboundNetworkEvents
| where url contains "CEO"
|  where referrer contains "https:framtidxdevcorp.com"
```
<br>

```
https://framtidxdevcorp.com/search%3DCEO%2527s%2Bdark%2Bsecrets
```
<br>


**Answer: dark secrets**<br><br>

**Q7. Did Johanna type in her credentials? yes/no.**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.6"
| where url contains "http://newdevelopmentupdates.org/public/signin"
```
<br>

Second result that is retrieved is below and shows the username and password entered. 

```
http://newdevelopmentupdates.org/public/signin?username=jokarlsson&password=**********
```
<br>

**Answer: yes**<br><br>



**Q8. When did the threat actor log in to Johanna’s machine?**<br><br>

```
AuthenticationEvents
| where username == "jokarlsson" 
| where timestamp > datetime(6/26/2024, 2:34:22 PM)
```
<br>

**Answer: 6/27/2024, 12:40:59 PM**<br><br>

**Q9. In which folder did they collect the incriminating files?**<br><br>

```
ProcessEvents
| where hostname == "BLVR-MACHINE"
| where process_name contains "powershell"
| where timestamp > datetime(6/26/2024, 2:34:22 PM)
```
<br>

```
Get-ChildItem -Path C:\Users\jokarlsson\Documents\Emails\* -Include *.eml, *.msg -Recurse | Copy-Item -Destination C:\Users\jokarlsson\Documents\StolenEmails\
```
<br>

**Answer: C:\Users\jokarlsson\Documents\StolenEmails\**<br><br>

**Q10. What command did they use to do this?**<br><br>

```
ProcessEvents
| where hostname == "BLVR-MACHINE"
| where process_name contains "powershell"
| where timestamp > datetime(6/26/2024, 2:34:22 PM)
```
<br>

**Answer: Compress-Archive -Path C:\Users\jokarlsson\Documents\StolenEmails\** -DestinationPath C:\Users\jokarlsson\Documents\StolenEmails.zip**<br><br>

**Q11. Those must have been some very important emails… Let’s see if you can find which one they were interested in. Johanna seems to have had a few email exchange with a very specific person. What is the email address of that person?**<br><br>

```
Email
| where sender == "johanna_karlsson@framtidxdevcorp.com"
| summarize NumOfEmails = count() by recipient
```
<br>
The top result shows Erik Stevens.<br><br>

**Answer: erik.stevens@valdoriapublicworks.gov**<br><br>


**Q12. How many emails total can you find between them?**<br><br>

```
Email
| where (sender has "johanna_karlsson@framtidxdevcorp.com" and recipient == "erik.stevens@valdoriapublicworks.gov") 
    or (sender has "erik.stevens@valdoriapublicworks.gov" and recipient == "johanna_karlsson@framtidxdevcorp.com")
```
<br>

**Answer: 6**<br><br>

**Q13. What is the mayor looking forward to?**<br><br>
From previous query subject lines.<br><br>

**Answer: We're going to make so much freaking money!**<br><br>

**Q14. What is the link Johanna shared with the mayor in her last email?**<br><br>
From query in question 12.<br><br>

**Answer: https://www.whyyoushoudntcareaboutnature.com**<br><br>


**Q15. When did this happen?**<br><br>

```
ProcessEvents
| where hostname == "BLVR-MACHINE"
| where timestamp > datetime(6/26/2024, 2:34:22 PM)
```
<br>

```
$emails = Get-ChildItem -Path C:\\Users\\jokarlsson\\Documents\\q\\*.eml;
$chunks = [System.Collections.Generic.List[System.Collections.Generic.List[System.IO.FileInfo]]]::new();
$chunkSize = 10;
for ($i = 0; $i -lt $emails.Count; $i += $chunkSize) {
  $chunks.Add($emails[$i..($i + $chunkSize - 1)]);
}
foreach ($chunk in $chunks) {
  $chunk | Compress-Archive -DestinationPath "C:\\Users\\jokarlsson\\Documents\\Chunk$($chunks.IndexOf($chunk)).zip";
}
```
<br>

**Answer: 7/8/2024, 2:41:47 PM**<br><br>

**Q16. How many chunks were the archive divided into?**<br><br>
From previous answer.<br><br>

```
$chunkSize = 10;
```
<br>

**Answer: 10**<br><br>

**Q17. The hacktivists sent the chunks to an email address they control. What is that email address?**<br><br>


**Answer: **<br><br>
**Q. **<br><br>


**Answer: **<br><br>
**Q. **<br><br>


**Answer: **<br><br>
**Q. **<br><br>


**Answer: **<br><br>
