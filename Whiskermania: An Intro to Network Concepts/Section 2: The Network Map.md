## Whiskermania: An Intro to Network Concepts: Section 2: The Network Map<br>
### **Summary**<br>
Let's start with the basics. You need to look like you know what you're doing, which means actually knowing what you're doing.
<br><br>
An IP address is like a mailing address for computers. Every device on a network needs one so other devices know where to send data. The format looks like this: 10.10.16.5. Four numbers separated by dots. Each number ranges from 0 to 255.
<br><br>
You'll see IP addresses constantly in network logs. They're how you identify which device did what.
<br><br>
What does IP stand for?
<br><br>

**Q1. What does IP stand for?**<br><br>

**Answer: Internet Protocol**<br><br>

**Q2. How many octets are in an IPv4 address?**<br><br>

**Answer: 4**<br><br>

**Q3. Is 10.10.16.5 a public or private IP address?**<br><br>

**Answer: Private**<br><br>

**Q4. Is 8.8.8.8 public or private?**<br><br>

**Answer: Public**<br><br>

**Q5. 192.168.1.1 is a common home router address. Public or private?**<br><br>

**Answer: Private**<br><br>

**Q6. 172.20.50.1. The private range for 172 is 172.16 through 172.31. This is 172.20, which falls in that range. Public or private?**<br><br>

**Answer: Private**<br><br>

**Q7. 52.214.98.1 is an AWS cloud server. 52 isn't in any private range. Public or private?**<br><br>

**Answer: Public**<br><br>

**Q8. "185.174.137.42 - WHO IS THIS? Check again." The handwriting gets more urgent toward the end. Jamie circled the IP twice. Is 185.174.137.42 public or private?**<br><br>

**Answer: Public**<br><br>

**Q9. How many VLANs (network zones) does Whiskers & Wonders have?**<br><br>
Using the query given.<br><br>

```
DeviceInfo
| summarize device_count=count() by vlan
| order by device_count desc
```
<br>

**Answer: 5**<br><br>

**Q10. Which VLAN has the most devices?**<br><br>

**Answer: workstations**<br><br>

**Q11. What is the IP address of the DonationPortal?**<br><br>

```
DeviceInfo
| where vlan == "dmz"
| project name, ip_address, host_type
```
<br>

**Answer: 10.10.0.3**<br><br>

**Q12. What is the IP address of MailServer01?**<br><br>

```
DeviceInfo
| where vlan == "servers"
| project name, ip_address
```
<br>

**Answer: 10.10.1.2**<br><br>

**Q13. What device is in the restricted zone?**<br><br>

```
DeviceInfo
| where vlan == "restricted"
| project name, ip_address, host_type
```
<br>

**Answer: DomainController**<br><br>

**Q14. What VLAN do IPs starting with 10.10.1 belong to?**<br><br>
From the question, a summary of IP ranges are given.<br><br>

- DMZ: 10.10.0.x
- Servers: 10.10.1.x
- Restricted: 10.10.2.x
- Workstations: 10.10.16.x
- 
**Answer: DomainController**<br><br>

**Q15. What IP range are workstations in? (format: 10.10.X)**<br><br>
From previous question, the IP range can be found.<br><br>

**Answer: 10.10.16**<br><br>

**Q16. What is the IP address of the DNS-Server?**<br><br>

```
DeviceInfo
| where name == "DNS-Server"
| project name, ip_address, vlan
```
<br>

**Answer: 10.10.1.7**<br><br>

**Q17. What table would show you DNS lookups?**<br><br>

**Answer: DnsEvents**<br><br>

**Q18. What zone contains the Domain Controller?**<br><br>
Referring back to the diagram from question 10 on the website.<br><br>

**Answer: restricted**<br><br>

**Q19. Type time to dig deeper to continue.**<br><br>

**Answer: time to dig deeper**<br><br>




