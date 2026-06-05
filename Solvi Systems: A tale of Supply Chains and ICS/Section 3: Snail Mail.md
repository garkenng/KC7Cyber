## Solvi Systems: A tale of Supply Chains and ICS: Section 3: Snail Mail<br>
### **Summary**<br>
Oh no! We received so many malicious emails. They weren't done after all!
<br><br>
Good news: we have new leads in our investigation.
Bad news: we have more investigating to do!
<br><br>
Let's explore these malicious emails that were sent by the adversary.
<br><br>

**Q1. How many emails associated with these domains did SolviSystem employees receive?**<br><br>
Using the previous query in question 13, section 2, shows how many results were returned.<br><br>

**Answer: 56**<br><br>

**Q2. How many distinct email addresses did the threat actor use?**<br><br>

```
Email
| where link contains "eco-awareness-update.net" or link contains "news-on-industry.com" or link contains "energy-trends4u.net"
| distinct sender
```
<br>

**Answer: 3**<br><br>

**Q3. How many distinct filenames were observed in the links in these emails?**<br><br>
The hint for this question is to use parse_path. This command allows you to extract parts of a directory path. In this case we need the file name in the link from the email.<br><br>

```
Email
| where link contains "eco-awareness-update.net" or link contains "news-on-industry.com" or link contains "energy-trends4u.net"
| extend ParsedFileName = parse_path(link).Filename
| extend ParsedFileName = parse_path(tostring(ParsedFileName)).Filename
| distinct tostring(ParsedFileName)
```
<br>

**Answer: 3**<br><br>

**Q4. How many different roles were targeted with these emails?**<br><br>
This question requires to break it down in two queries. First need to search for email addresses that contain the filenames / links what are malicious. Then these email addresses are passed into the Employees table to determine what roles they hold.<br><br>

```
let EmailWithBadLinks = 
Email
| where link contains "eco-awareness-update.net" or link contains "news-on-industry.com" or link contains "energy-trends4u.net"
| extend ParsedFileName = parse_path(link).Filename
| extend ParsedFileName = parse_path(tostring(ParsedFileName)).Filename
| where link contains ParsedFileName
| distinct recipient;
Employees
| where email_addr in (EmailWithBadLinks)
| distinct role
| count
```
<br>

**Answer: 5**<br><br>

**Q5. How many Customer Support Specialist employees received malicious emails?**<br><br>

**Answer: 27**<br><br>
