## Titan Shield: A showcase of Microsoft Defender XDR: Section 5: A Heartbreak<br>
### **Summary**<br>
You look through the logs, and it doesnt seem like Taylor went out of his way to search and download this file. Maybe he just clicked a link in an email.
<br><br>
Let's look for this URL to see if it was delivered in any emails.
<br><br>


**Q1. Who sent the email?**<br><br>

```
Email
| where link has "https://healthylifestyle.com/share/New_Diet_Plan_For_My_Love.xlsx"
```
<br>

**Answer: marcella_flores@gmail.com**<br><br>
