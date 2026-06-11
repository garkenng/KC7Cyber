## KQL 201: An Intermediary Course on KQL: Section 2: Aggregation<br>
### **Summary**<br>
With so many results returned, some attacks blend in with normal activity. That's why aggregation is key to spotting unusual patterns.
<br><br>
A single failed login isn't suspicious. But 100 failed logins from one IP? That's worth investigating.
<br><br>
The summarize operator transforms raw events into meaningful insights by grouping and counting data.
<br><br>

**Q12. Enter show me the numbers to continue**<br><br>
**Answer: show me the numbers**<br><br>

**Q13. How many unique IP addresses successfully logged in?**<br><br>

```
AuthenticationEvents
| where result == "Successful Login"
| summarize total_logins = count() by src_ip
```
<br>

**Answer: 641**<br><br>

**Q14. Which IP had the highest count of observed logins?**<br><br>
From previous query.<br><br>

**Answer: 10.10.0.10**<br><br>


**Q15. Which IP did the account admiassi_local_admin login from the most?**<br><br>
From query in question 13.<br><br>

**Answer: 10.10.0.10**<br><br>

```
ProcessEvents
| summarize distinctprocess = count()by process_name
```

**Answer: 98**<br><br>


**Q17. How many IP addresses failed to login to more than one account?**<br><br>

```
AuthenticationEvents
| where result == "Failed Login"
| summarize unique_accounts = dcount(username) by src_ip
| where unique_accounts > 1
```
<br>

**Answer: 6**<br><br>


**Q18. Which IP was seen successfully logging into the most accounts?**<br><br>
**Answer:**<br><br>


**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>
**Q.**<br><br>
**Answer:**<br><br>

