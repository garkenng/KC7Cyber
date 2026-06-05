## Solvi Systems: A tale of Supply Chains and ICS: Section 3: Snail Mail<br>
### **Summary**<br>
Oh no! We received so many malicious emails. They weren't done after all!
<br><br>
Good news: we have new leads in our investigation. Bad news: we have more investigating to do!
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
This question requires to break it down in two queries. First need to search for email addresses that contain the filenames / links that are malicious. Then these email addresses are passed into the Employees table to determine what roles they hold.<br><br>

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
Using the previous query and modify the second query to show only customer support specialist.<br><br>

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
| where role == "Customer Support Specialist"
| count 
```
<br>

**Answer: 27**<br><br>

**Q6. Among these job roles, which word is shared by three of them?**<br><br>

```
Employees
| extend JobKeywords = split(role, " ") 
| mv-expand JobKeywords to typeof(string)        
| summarize 
    Count = count(), 
    DifferentRoles = make_set(role) 
    by JobKeyword = tolower(JobKeywords)
| where Count == 3
```
<br>
Results produced by above query.<br><br>

```
["DOCKS ICS Security Lead","Project Manager for Docks ICS","Docks Customer Success Manager"]
```
<br>

**Answer: Docks**<br><br>

**Q7. What was the timestamp of the first email the threat actor sent?**<br><br>
Running a modified query from question 5.<br><br>

```
Email
| where link contains "eco-awareness-update.net" or link contains "news-on-industry.com" or link contains "energy-trends4u.net"
| extend ParsedFileName = parse_path(link).Filename
| extend ParsedFileName = parse_path(tostring(ParsedFileName)).Filename
| where link contains ParsedFileName
```
<br>
First result is the timestamp of the first email sent by the threat actor.<br><br>

**Answer: 5/1/2024, 3:51:41 PM**<br><br>

**Q8. What is the recipient's email address?**<br><br>
Answer retrieved from previous query.<br><br>

**Answer: carla_wharton@solvisystems.com**<br><br>

**Q9. What is that employee's name?**<br><br>

```
Employees
| where email_addr == "carla_wharton@solvisystems.com"
```
<br>

**Answer: Carla Wharton**<br><br>

**Q10. What was the sender address of that email?**<br><br>
Using the query from question 7, the senders address can be found.<br><br>

**Answer: news@eco-awareness-updates.net**<br><br>

**Q11. What was the reply to address?**<br><br
Using the query from question 7.<br><br>

**Answer: electric_updates@gmail.com**<br><br>

**Q12. What was the subject of that email?**<br><br>
Using the query from question 7.<br><br>

**Answer: [EXTERNAL] Business Opportunity: Two major energy companies merging**<br><br>

**Q13. What link was observed in the email?**<br><br>
Using the query from question 7.<br><br>

**Answer: http://news-on-industry.com/search/online/files/public/Energy_Industry_Trends_2024_4_Solvi.docx**<br><br>

**Q14. Did Carla click on the link in email? If so when?**<br><br>
The url for the link can be used from question 13 and full name from question 9. Can find Carla IP address using this information by querying the OutboundNetworkEvents table.<br><br>


**Answer: **<br><br>
