## Cowboy Couture: A Steampunk Space Adventure: Section 4: Cowhands-On-Keyboard<br>
### Summary
You thought you had it all figured out, but this new discovery has left you confused. What does this mean? You want to reach out to Wade for help, but you remember that he's about to give his closing keynote. Frustrated, you sift through your CISSP notes, but can't find anything there to help you think through this problem.
<br><br>
Then, you remember some of the questions you answered earlier in this training module and it suddenly hits you. You know just what to do!
<br><br>

**Q1. Enter Anyone can do it! to continue**<br>
**Answer: Anyone can do it!**<br><br>

**Q2. How many succesful logins were made from that IP?**<br>

```
AuthenticationEvents
| where src_ip == "192.124.249.15" and result == "Successful Login"
| count
```
<br>

**Answer: 2**<br><br>

**Q3. What is the username for the other employee that this IP was used to log into?**<br>

```
AuthenticationEvents
| where src_ip == "192.124.249.15" and result == "Successful Login"
```
<br>

Two hostnames are returned.<br><br>

```
JHTJ-DESKTOP
ITCK-MACHINE
```
<br>
Run search for the username for hostname JHTJ-DESKTOP.<br><br>

```
Employees
| where hostname == "JHTJ-DESKTOP"
```
<br>

**Answer: jahartley**<br><br>


**Q4. What is this employee's role?**<br>
From previous query.<br><br>

**Answer: CEO**<br><br>

**Q5. Enter the timestamp for when the attacker established persisitence.**<br>

```
ProcessEvents
|where hostname == "JHTJ-DESKTOP"
| where timestamp between 
        (datetime(2024-09-19T06:25:59Z) .. datetime(2024-09-20T15:25:27Z))
```
<br>

One result is of interest.<br><br>

```
net user backdooradmin CowboyBandits123! /add && 
net localgroup administrators backdooradmin /add && 
echo "User 'backdooradmin' added to Administrators group."
```
<br>

**Answer: 9/20/2024, 4:39:09 AM**<br><br>


**Q6. How many domains does the 192.124.249.15 IP resolve to?**<br>

```
PassiveDns
| where ip == "192.124.249.15"
| distinct domain
```
<br>

**Answer: 2**<br><br>


**Q7. What newly uncovered IP resolves to the secure-celestial.com domain?**<br>

```
 PassiveDns
 | where domain in ("secure-celestial.com",
   "celestialcowboy-support.com")
```
<br>

**Answer: 142.250.191.78**<br><br>


**Q8. What is the name of the next domain that you've uncovered?**<br>

```
let all_ips = PassiveDns
|where domain in ("secure-celestial.com", 
    "celestialcowboy-support.com")
|distinct ip;
PassiveDns
| where ip in (all_ips)
|distinct domain
```
<br>

**Answer: cccouture-hr-update.com**<br><br>


**Q9. Is there any evidence of network traffic to any of those domains? (Yes/No)**<br>

```
OutboundNetworkEvents
| where url has_any ("cccouture-hr-update.com", 
 "celestialcowboy-support.com",
 "secure-celestial.com")
```
<br>

**Answer: Yes**<br><br>


**Q10. What is the subject of the email sent to Megan Lucia?**<br>

```
 Email
 | where link has_any ("cccouture-hr-update.com", 
 "celestialcowboy-support.com",
 "secure-celestial.com")
```
<br>

**Answer: URGENT: From your CEO - Immediate Action Required: You are getting promoted Cowboy!!!!**<br><br>


**Q11. Which Backdoors & Breaches initial compromise card was played here?**<br>

**Answer: Phish **<br><br>


**Q12. Enter Happy Trails to complete this investigation.**<br>
**Answer: Happy Trails**<br><br>
