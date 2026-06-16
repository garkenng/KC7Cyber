## KQL 301: Section 4: Text Processing<br>

**Q1. How many characters are in the longest email address username?**<br><br>

```
Employees
| parse email_addr with username "@" *
| project username, UserNameLength = strlen(username)
```
<br>

**Answer: 17**<br><br>

**Q2. What is the first filename created on pawilson's machine?**<br><br>

```
FileCreationEvents
| where username == 'pawilson'
| extend parts = split(path, "\\")
| extend lastURL = array_length(parts) - 1
| extend lastURLValue = parts[LastIndex]
```
<br>

**Answer: spotify.exe**<br><br>


**Q3. What domain sent the most emails?**<br><br>

```
Email
| extend sender_domain = split(sender, "@")[1]
| summarize count() by tostring(sender_domain)
| sort by count_ desc
```
<br>

**Answer: whiskersandwonders.org**<br><br>


**Q4. How many unique domains were visited?**<br><br>

```
ProxyEvents
| distinct domain
```
<br>

**Answer: 488**<br><br>

