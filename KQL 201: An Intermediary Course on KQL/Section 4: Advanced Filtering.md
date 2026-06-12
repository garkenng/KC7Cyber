## KQL 201: An Intermediary Course on KQL: Section 4: Advanced Filtering<br>
### **Summary**<br>

**Q38. How many events originate from IPs starting with 10.10.1.4?**<br><br>

```
AuthenticationEvents
| where src_ip startswith "10.10.1.4"
```
<br>

**Answer: 633**<br><br>

**Q39. How many emails were sent with links ending with .docx**<br><br>

```
Email
| where link contains ".docx"
```
<br>

**Answer: 273**<br><br>

**Q40. Using the query below as a template, how many unique sender domains were observed that were not one of the following?**<br><br>

**Answer: **<br><br>

**Q41.**<br><br>

**Answer: **<br><br>

**Q42.**<br><br>

**Answer: **<br><br>
