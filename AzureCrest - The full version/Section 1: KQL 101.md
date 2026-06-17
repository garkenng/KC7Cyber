## AzureCrest - The full version: Section 1: KQL 101<br>
### **Section 1**<br>
### **Summary**<br>
Welcome to Azure Crest Hospital!
<br><br>
Azure Crest Hospital, known for its wide range of medical services, is a major healthcare provider, supported by a large, dedicated team of medical and administrative professionals.
<br><br>
Given the tough economic environment, Azure Crest has been on a mission to improve financial performance by reducing costs, and to think of creative ways to streamline operations.
<br><br>
One of these resulting measures is a groundbreaking new Enterprise Resource Planning (ERP) system developed by the hospital's Database Administrator, which centralizes all patient records and information used by the hospital onto one single server.
<br><br>
Your mission is crucial: to detect and thwart any cyber threats against Azure Crest Hospital, maintaining its status as a trusted healthcare provider.
<br><br>

**Q1. Enter ready to get started!**<br><br>

**Answer: ready**<br><br>

**Q2. Type "done" to earn credit for this question.**<br><br>

**Answer: done**<br><br>

**Q3. How many employees work at Azure Crest Hospital?**<br><br>

```
Employees
| count
```
<br>

**Answer: 250**<br><br>

**Q4. What is the Chief Financial Officer's name?**<br><br>

```
Employees
| where role == "Chief Financial Officer"
```
<br>

**Answer: Penny Pincher**<br><br>

**Q5. How many emails did Penny Pincher receive?**<br><br>

```
Email
| where recipient == "penny_pincher@azurecresthospital.med"
| count
```
<br>

**Answer: 30**<br><br>


**Q6. How many distinct senders were seen in the email logs from pharmabest.net?**<br><br>

```
Email
| where sender has "pharmabest.net"
| distinct sender
| count
```
<br>

**Answer: 236**<br><br>

**Q7. How many distinct websites did “Penny Pincher” visit?**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.1"
| distinct url
| count 
```
<br>

**Answer: 68**<br><br>


**Q8. How many distinct domains in the PassiveDns records contain the word “health”?**<br><br>

```
PassiveDns
| where domain contains "health"
| distinct domain
| count
```
<br>

**Answer: 28**<br><br>

**Q9. What IPs did the domain “bit.ly” resolve to (enter any one of them)?**<br><br>

```
PassiveDns
| where domain == "bit.ly"
| distinct ip
```
<br>

**Answer: 134.177.143.174**<br><br>

**Q10. How many distinct URLs did employees with the first name "Mary" Visit?**<br><br>

```
let mary_ips = 
Employees
| where name has "Mary"
| distinct ip_addr;
OutboundNetworkEvents
| where src_ip in (mary_ips)
| distinct url
| count
```
<br>

**Answer: 119**<br><br>


**Q11. How many authentication attempts did we see to the accounts of employees with the first name Mary?**<br><br>

**Answer: 180**<br><br>


**Q12. Enter "ready" to earn credit for this question.**<br><br>

**Answer: ready**<br><br>
**Q13. **<br><br>

**Answer: **<br><br>
**Q. **<br><br>

**Answer: **<br><br>
