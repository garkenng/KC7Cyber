## Critical Compromise In Chicago - ICS: Section 2: Phish and Chips
### Summary
The investigation is about to get tougher.😱
<br><br>
You’ve traced the malicious file back to a user interaction, but this was much more complex than a simple mistake. The attacker initiated a sophisticated phishing campaign, targeting multiple employees before launching a second, more focused phishing attack on the user who ultimately opened Urgent_Cyber_Threat_Alert.zip.
<br><br>
Now it's time for you to find out how they did it. Are you up for the challenge?
<br><br>

**Q1. Enter Phish and Chips to continue.**<br><br>

**Answer: Phish and Chips**<br><br>

**Q2. Which sender address did the threat actor use to target the highest number of employees?**<br><br>
Run a search for recipient employees and with the subject used in the original phishing email. <br><br>

```
Email
| where subject contains "Grid Security Update Required"
| where recipient contains "chicagopowergrid"
```
<br>
The results show 4 email addresses that could have potentially emailed employees.<br><br>

```
joseph_eisenman@chicagopowergrid.com
thresher_libero@hotmail.com
elizabeth_nunmaker@chicagopowergrid.com
chopping_asbestosis@verizon.com
```
<br>
Run a search on Email table using the above addresses as sender.<br><br>

```
Email
| where sender in ("joseph_eisenman@chicagopowergrid.com", "thresher_libero@hotmail.com", "elizabeth_nunmaker@chicagopowergrid.com", "chopping_asbestosis@verizon.com")
| where recipient contains "chicagopowergrid"
```
<br>
Searching through the results, a subject line seems of interest.<br><br>

```
[EXTERNAL] Critical: Severe Security Breach Detected - Immediate Action Required
```
<br>
Run a search with that subject line.<br><br>

```
Email
| where subject == "[EXTERNAL] Critical: Severe Security Breach Detected - Immediate Action Required"
```
<br>
The majority of the emails were sent by thresher_libero@hotmail.com.<br><br>

**Answer: thresher_libero@hotmail.com**<br><br>

**Q3. What threat actor controlled IP was used to log in to the most accounts?**<br><br>
Referring back to question 17 in section 1, Joseph Eisenman was the user who was originally compromised. Run a search for this username in authentication events to see the IP address they are using.<br><br>

```
AuthenticationEvents
| where username == "joeisenman"
```
<br>

Scrolling through the results, there is one user agent that stands out.<br><br>

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_1; rv:1.9.5.20) Gecko/2021-05-22 21:31:56 Firefox/10.0
```
<br>
The threat actor is likely associated with this result.<br><br>

**Answer: 87.250.252.242**<br><br>


**Q4. **<br><br>

**Answer: **<br><br>
**Q5. **<br><br>

**Answer: **<br><br>
**Q6. **<br><br>

**Answer: **<br><br>
**Q7. **<br><br>

**Answer: **<br><br>
**Q8. **<br><br>

**Answer: **<br><br>
**Q9. **<br><br>

**Answer: **<br><br>
**Q10. **<br><br>

**Answer: **<br><br>


