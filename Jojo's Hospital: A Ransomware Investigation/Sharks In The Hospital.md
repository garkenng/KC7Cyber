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
