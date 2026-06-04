

## Solvi Systems: A tale of Supply Chains and ICS: Section 1: KQL 101<br>
### **Summary**<br>
Welcome to Solvi Systems!
<br><br>
Solvi Systems is a software company that plays a pivotal role in shaping the future of the energy sector in South Africa. At the heart of Solvi Systems' operations is its Docks software, a critical component used by major power and utility companies.
<br><br>
Solvi Systems' influence extends beyond national borders. The company plays a crucial role in regional stability, as South Africa exports power to neighboring states like Mozambique, Eswatini, Zimbabwe, and Namibia. This interconnectedness means that any vulnerability or disruption in South Africa's energy infrastructure, and by extension Solvi Systems' software, doesn't just affect one nation but echoes across the region.
<br><br>
Given this key role, Solvi Systems is a prime target for cyber adversaries. You've been hired to identify any intrusions against this company.<br><br>

**Q1 Enter ready to get started.**<br><br>

**Answer: ready**<br><br>

**Q2 Type "done" to earn credit for this question.**<br><br>

**Answer: done**<br><br>

**Q3 How many employees work at Solvi Systems?**<br><br>

```
Employees
| count
```
<br>

**Answer: 500**<br><br>

**Q4. What is the CTO's name?**<br><br>

```
Employees
| where role == "CTO"
```
<br>

**Answer: Alexis Khoza**<br><br>

**Q5. How many emails did Alexis Khoza receive?**<br><br>
The email address can be retrieved from the previous query.<br><br>

```
Email
| where recipient == "alexis_khoza@solvisystems.com"
| count
```
<br>

**Answer: 31**<br><br>

**Q6. How many distinct senders were seen in the email logs from eskom.co.za?**<br><br>

```
Email
| where sender has "eskom.co.za"
| distinct sender
| count
```
<br>

**Answer: 745**<br><br>

**Q7. How many distinct websites did “Alexis Khoza” visit?**<br><br>
Alexis IP address found from question 4.<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.7"
| distinct url
| count
```
<br>

**Answer: 72**<br><br>

**Q8. How many distinct domains in the PassiveDns records contain the word “real”?**<br><br>

```
PassiveDns
| where domain contains "real"
| distinct domain
| count
```
<br>

**Answer: 19**<br><br>

**Q9. What IPs did the domain “bit.ly” resolve to (enter any one of them)?**<br><br>

```
PassiveDns
| where domain == "bit.ly"
| distinct ip
```
<br>

**Answer: 30.99.71.8**<br><br>

