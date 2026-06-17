## Frognado In Valdoria: A Political Mystery: Section 3: Alright It's Definitely An Angry Frog Or Two<br>
### **Summary**<br>
"My name is Erik Bjorn, I’m a Chief Architect here."
<br><br>
Already you like this guy better than the creepy mute man. He explains that he had wanted to go over some details on the construction plans for the mall, but when he opened the file, he was greeted by, well, “just see for yourself.”
<br><br>
You manage to keep your face perfectly blank this time (but, yes, you laugh internally). This confirms your suspicion that the threat actor went beyond Anita’s machine. The frogs are furious.
<br><br>
You thank Erik for the information, telling him your investigation will go faster thanks to him. He nods gravely. He needs to get in touch with the other Chief Architect who is on vacation to inform her of the situation (“she’s not gonna be happy, those architectural plans were her babies”), so you leave him to it and go back to your desk.
<br><br>
Thanks to your work on Anita’s case, you have an idea of how it all started, you just need to confirm it. And from there you can just follow the breadcrumbs.
<br><br>


**Q1. What is the name of Erik Bjorn’s colleague?**<br><br>

```
Employees
| where role == "Chief Architect"
| where name !contains "Erik"
```
<br>

**Answer: Sofia Lindgren**<br><br>

**Q2. You check to see if the Chief Architects received emails from the same internal address you found when investigating Anita. What is the subject of these emails?**<br><br>

```
Email
| where recipient == "sofia_lindgren@framtidxdevcorp.com"
| where sender == "alex_johnson@framtidxdevcorp.com"
```
<br>

**Answer: Important: Architectural Plan Changes**<br><br>

**Q3. Which domain is the page hosted on?**<br><br>
From previous query.<br>

**Answer: greenprojectnews.net**<br><br>

**Q4. What type of phishing attack is this?**<br><br>

**Answer: spear phishing**<br><br>

**Q5. How many distinct pages on the company’s website did the threat actor browse to?**<br><br>

```
let WebPagesVisited = PassiveDns
    | where domain == "newdevelopmentupdates.org"
    | distinct ip;
InboundNetworkEvents
| where src_ip in (WebPagesVisited)
| distinct url
```
<br>

**Answer: 78**<br><br>

**Q6. Which job related referrer returned the most results?**<br><br>

```
let WebPagesVisited = PassiveDns
    | where domain == "newdevelopmentupdates.org"
    | distinct ip;
InboundNetworkEvents
| where src_ip in (WebPagesVisited)
| where referrer contains "https://"
| summarize total = count() by referrer
```
<br>

**Answer: https://www.valdorianjobs.com**<br><br>


**Q7. Did any of them try to log in to that actor controlled page? If only one of them did, answer with their name, if both did, type both.**<br><br>

```
OutboundNetworkEvents
| where src_ip in ("10.10.0.18", "10.10.0.3")
| where url contains "greenprojectnews.net"
| distinct src_ip
```
<br>

**Answer: both**<br><br>


**Q8. What time did they manage to log in to Sofia’s machine?**<br><br>

```
let SofiaLogin = PassiveDns
    | where domain == "greenprojectnews.net"
    | distinct ip;
AuthenticationEvents
| where src_ip in (SofiaLogin)
| where username == "solindgren"
| where result == "Successful Login"
```
<br>

**Answer: 6/27/2024, 10:41:38 AM**<br><br>

**Q9. What is the first Powershell cmdlet used to delete something from Erik and Sofia’s machines?**<br><br>
To delete a file from powershell cmdlet, the command would be 'Remove-Item'. Lets find an entry for that on their machines.<br><br>

```
ProcessEvents
| where hostname in ("LRJP-DESKTOP", "VJVS-MACHINE")
| where process_commandline contains "Remove-Item "
```
<br>

Two results are returned. One for each user / machine.<br><br>

```
Remove-Item C:\Users\solindgren\Documents\SuperImportantMallProjectArchitecturalPlans.docx
```
<br>

**Answer: Remove-Item**<br><br>

**Q10. What is the name of the file that was deleted?**<br><br>

**Answer: SuperImportantMallProjectArchitecturalPlans.docx**<br><br>

**Q11. What is the name of the file they downloaded?**<br><br>

```
ProcessEvents
| where hostname in ("LRJP-DESKTOP", "VJVS-MACHINE")
| where process_name contains "powershell"
```
<br>
Looking through the result, there is one result that appears to be of interest.<br><br>

```
Invoke-WebRequest -Uri https://newdevelopmentupdates.org/fake_plans.docx -OutFile C:\Users\erbjorn\Documents\fake_plans.docx
```
<br>

The Invoke-Web is a powershell cmdlet to send requests to web pages / services.<br><br>

**Answer:  fake_plans.docx**<br><br>


**Q12. Which domain hosted that file?**<br><br>

**Answer: newdevelopmentupdates.org**<br><br>

**Q13. What Powershell cmdlet did the attackers use to rename the downloaded file?**<br><br>

```
Rename-Item -Path C:\Users\erbjorn\Documents\fake_plans.docx -NewName SuperImportantMallProjectArchitecturalPlans.docx
```
<br>

**Answer: Rename-Item**<br><br>

**Q14. What was the file renamed to?**<br><br>

**Answer: SuperImportantMallProjectArchitecturalPlans.docx**<br><br>

**Q15. According to MITRE, what kind of impact is this an example of?**<br><br>

**Answer: Data Manipulation**<br><br>
