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

```
AuthenticationEvents
| where result == "Successful Login"
| summarize unique_accounts = dcount(username) by src_ip
| where unique_accounts > 1
```
<br>

**Answer: 10.10.0.75**<br><br>


**Q19. How many unique passwords were used in failed logins between May 1-7, 2024?**<br><br>

```
AuthenticationEvents
| where timestamp between (datetime(2024-05-01) .. datetime(2024-05-07))
| where result == "Failed Login"
| summarize count() by password_hash
```
<br>

**Answer: 2050**<br><br>

**Q20. On hostname 48NM-LAPTOP, how many unique passwords were used in failed logins between May 1-7, 2024?**<br><br>

```
AuthenticationEvents
| where timestamp between (datetime(2024-05-01) .. datetime(2024-05-07))
| where hostname == "48NM-LAPTOP"
| where result == "Failed Login"
| summarize count() by password_hash
```
<br>

**Answer: 2**<br><br>


**Q21. How many passwords were used 10 or more times?**<br><br>

```
AuthenticationEvents
| where timestamp between (datetime(2024-05-01) .. datetime(2024-05-07))
| where result == "Failed Login"
| summarize count() by password_hash
| sort by count_ desc
| where count_ >= 10
```
<br>

**Answer: 5**<br><br>


**Q22. How many passwords were used only once?**<br><br>

```
AuthenticationEvents
| where timestamp between (datetime(2024-05-01) .. datetime(2024-05-07))
| where result == "Failed Login"
| summarize count() by password_hash
| sort by count_ desc
| where count_ == 1
```
<br>

**Answer: 2018**<br><br>

**Q23. Enter spray detected to continue.**<br><br>

**Answer: spray detected **<br><br>

**Q24. How many distinct passwords were used against more than 10 accounts?**<br><br>

```
AuthenticationEvents
| where timestamp between (datetime(2024-05-01) .. datetime(2024-05-07))
| where result == "Failed Login"
| summarize unique_accounts = dcount(username) by password_hash
| sort by unique_accounts desc
| where unique_accounts > 10
```
<br>

**Answer: 0**<br><br>


**Q25.**<br><br>
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

