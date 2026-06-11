## KQL 201: An Intermediary Course on KQL: Section 1: Time-Based Filtering<br>
### **Summary**<br>
You've built a strong foundation in KQL 101, and now it's time to level up!
<br><br>
In KQL 201, you'll learn:
<br><br>
Time Analysis - Filter events by date ranges, spot patterns by hour, and track how long attacks lasted using startofday(), between, and bin().
<br><br>
Aggregation - Go beyond simple counts with dcount() to find unique values, min() and max() to track timelines, and make_set() to group related indicators.
<br><br>
Data Transformation - Clean up output with project, add calculated columns with extend, and flag suspicious activity with iff() and case().
<br><br>
Advanced Filtering - Search smarter with startswith, endswith, has_any, and exclude noise with !in.
<br><br>
Along the way, we'll investigate a password spray attack and use these techniques to uncover the attacker's patterns.
<br><br>

**Q1. Enter level up to continue.**<br><br>

**Answer: level up**<br><br>

**Q2. Enter timing is everything to continue.**<br><br>
**Answer: timing is everything**<br><br>

**Q3. How many rows are returned from the query above?**<br><br>

```
ProcessEvents
| where timestamp > datetime(2024-06-17T14:49:02Z)
```
<br>

**Answer: 382**<br><br>

**Q4. Enter start of day to continue.**<br><br>

**Answer: start of day**<br><br>

**Q5. How many authentication attempts were made on May 1, 2024?**<br><br>

```
AuthenticationEvents
| where timestamp >= datetime(05/01/2024)
| where timestamp <= datetime(05/02/2024)
```
<br>

**Answer: 673**<br><br>


**Q6. The endofday() function rounds timestamps up to 11:59:59.999 PM. Combined with <=, you can include the entire final day in a range. This finds all failed logins on or before May 07, 2024. How many rows are returned?**<br><br>

```
AuthenticationEvents
| where timestamp <= endofday(datetime(2024-05-07))
| where result == "Failed Login"
```
<br>

**Answer: 2584**<br><br>

**Q7. How many login attempts failed on or before June 19, 2024?**<br><br>

```
AuthenticationEvents
| where timestamp <= endofday(datetime(2024-06-19))
| where result == "Failed Login"
```
<br>

**Answer: 17884**<br><br>


**Q8. Enter between the dates to continue.**<br><br>

**Answer: between the dates**<br><br>

**Q9. How many login attempts failed between June 1, 2024 and June 7, 2024?**<br><br>

```
AuthenticationEvents
| where timestamp between (datetime(2024-06-01) .. datetime(2024-06-07))
| where result == "Failed Login"
```
<br>

**Answer: 2259**<br><br>



**Q10. Enter time is relative to continue.**<br><br>
**Answer: time is relative**<br><br>

**Q11. On May 12, 2024, which hour saw the most failed logins? (#am or #pm)**<br><br>

```
AuthenticationEvents
| where result == "Failed Login"
| summarize hourly_failures = count() by bin(timestamp, 1h)
| order by timestamp asc
```
<br>

**Answer: 2pm**<br><br>

**Q12. Enter show me the numbers to continue.**<br><br>

**Answer: show me the numbers**<br><br>

