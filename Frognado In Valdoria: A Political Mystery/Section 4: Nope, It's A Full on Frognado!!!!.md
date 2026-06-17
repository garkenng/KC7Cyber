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
