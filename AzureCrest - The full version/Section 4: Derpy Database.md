## AzureCrest - The full version: Section 4: Derpy Database<br>

**Q1. This Twitter user, also known as "Hutch", co-authored the paper that introduced the Cyber Kill Chain to information security. (enter their @ username)**<br><br>

**Answer: @killchain**<br><br>

**Q2. What is the first step of the Cyber Kill Chain?**<br><br>


**Answer: Reconnaissance**<br><br>

**Q3. How many records are there of the threat actor browsing the Azure Crest Hospital's website?**<br><br>
First is to look for url with the keyword search in, to see what searches have been carried out on the hospital website.<br><br>

```
InboundNetworkEvents
| where url contains "search"
```
<br>

Looking at the different user agents, one agent is of interest.<br><br>

```
Opera/9.63.(Windows CE; lb-LU) Presto/2.9.161 Version/12.00
```
<br>

Run search for inbound traffic with that user agent.<br><br>

```
InboundNetworkEvents
| where user_agent == "Opera/9.63.(Windows CE; lb-LU) Presto/2.9.161 Version/12.00"
```
<br>

Looking through the url column, the threat actor is searching for information which not deemed normal.<br><br>

```
How many money does Azure Crest Hospital have
Azure Crest Hospital financial statements
```
<br>

**Answer: 32**<br><br>


**Q4. What article did they read about personnel changes at the hospital? (provide full url)**<br><br>
Looking through links visited on hospital website.<br><br>

**Answer: https://azurecresthospital.med/news/half-of-it-department-fired**<br><br>

**Q5. Which employee was hired as part of an effort to reduce costs?**<br><br>
Looking through links visited on hospital website.<br><br>

```
https://azurecresthospital.med/news/roy-trenemman-joins-azure-crest-to-save-money-on-erp-systems
```
<br>

**Answer: Roy Trenneman**<br><br>


**Q6. What article did Azure Crest publish about building one's own stuff instead of paying for it? (provide the full url)**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
**Q.**<br><br>


**Answer: **<br><br>
