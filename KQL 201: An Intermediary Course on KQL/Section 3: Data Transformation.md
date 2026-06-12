## KQL 201: An Intermediary Course on KQL: Section 3: Data Transformation<br>
### **Summary**<br>
Now let's learn how to shape your query output.
<br><br>
When you run a query, you get every column in the table. But often you only care about a few fields. The project operator selects which columns to display:
<br><br>
This returns only the three columns you need, making output cleaner and easier to read.
<br><br>

**Q33. Enter project it to continue**<br><br>

**Answer: project it**<br><br>

**Q34. Enter rename columns to continue.**<br><br>

**Answer: rename columns**<br><br>

**Q35. Enter extend it to continue.**<br><br>

**Answer: extend it**<br><br>

**Q36. How many authentication events occurred during off-hours?**<br><br>

```
AuthenticationEvents
| extend hour = hourofday(timestamp)
| where hour < 6 or hour >= 18
| count
```
<br>

**Answer: 3**<br><br>

**Q37. Enter conditional logic to continue.**<br><br>

**Answer: conditional logic**<br><br>

