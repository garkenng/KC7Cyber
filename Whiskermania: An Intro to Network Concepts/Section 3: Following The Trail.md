## Whiskermania: An Intro to Network Concepts: Section 3: The Following The Trail<br>
### **Summary**<br>
With Morgan gone, you have time to dig into Jamie's notebook properly.
<br><br>
There's a page titled "Network Flow Analysis" with a note at the top: "Every connection has two endpoints: source IP + port → destination IP + port"
<br><br>
You know about IP addresses now. But what's a port?
<br><br>
Think of it this way: the IP address gets you to the right building, but the port gets you to the specific apartment. A server might run multiple services, and each service listens on a different port.
<br><br>

          SERVER: 142.250.80.46
     ┌─────────────────────────────┐
     │  ┌─────┐ ┌─────┐ ┌─────┐   │
     │  │ :22 │ │ :80 │ │:443 │   │
     │  │ SSH │ │HTTP │ │HTTPS│   │
     │  └─────┘ └─────┘ └─────┘   │
     └─────────────────────────────┘
<br>

Port numbers range from 0 to 65535.

**Q1. What is the maximum port number?**<br><br>

**Answer: 65535**<br><br>

**Q2. What port number is used for HTTPS?**<br><br>

**Answer: 443**<br><br>

**Q3. What port number is used for DNS?**<br><br

**Answer: 53**<br><br>

**Q4. What port number is used for SSH?**<br><br

**Answer: 22**<br><br>

**Q5. What port number is used for RDP?**<br><br

**Answer: 3389**<br><br>

**Q6. What destination port has the most traffic?**<br><br>

```
NetworkFlow
| summarize traffic=count() by dest_port
| order by traffic desc
| take 5
```
<br>

**Answer: 25**<br><br>

**Q7. What does SMTP stand for?**<br><br>

**Answer: Simple Mail Transfer Protocol**<br><br>

**Q8. What does TCP stand for?**<br><br>

**Answer: Transmission Control Protocol**<br><br>

**Q9. What does UDP stand for?**<br><br>

**Answer: User Datagram Protocol**<br><br>

**Q10. What protocol does DNS primarily use?**<br><br>

```
NetworkFlow
| where dest_port == 53
| summarize count() by protocol
```
<br>

**Answer: UDP**<br><br>

**Q11. What protocol carries the majority of network traffic on this network?**<br><br>

```
NetworkFlow
| summarize count() by protocol
| order by count_ desc
```
<br>

**Answer: TCP**<br><br>

**Q12. Morgan pokes their head back in. "Still alive in here?"
<br><br>
"Just reviewing the network architecture," you say, which is technically true.
<br><br>
"Uh huh." Morgan doesn't look entirely convinced, but they're too busy to press. "Holler if you need anything. I'll be dealing with the new kitten intake."
<br><br>
Biscuits, still on the desk, yawns.
<br><br>
Type totally normal to continue.**
<br><br>

**Answer: totally normal**<br><br>

**Q13. What does DNS stand for?**<br><br>

**Answer: Domain Name System**<br><br>

**Q14. What column contains the domain name that was looked up?**<br><br>

```
DnsEvents
| take 5
| project timestamp, client_ip, query_name, resolved_ips, dns_server
```
<br>

**Answer: query_name**<br><br>

**Q15. What type of DNS record maps a domain to an IPv4 address?**<br><br>

**Answer: A**<br><br>

**Q16. What does TTL stand for?**<br><br>

**Answer: Time To Live**<br><br>

**Q17. Type following the breadcrumbs to continue.**<br><br>

**Answer: following the breadcrumbs**<br><br>

**Q18. What IP address did docs.google.com resolve to?**<br><br>

```
DnsEvents
| where query_name == "docs.google.com"
| where query_type == "A"
| project timestamp, client_ip, query_name, resolved_ips
| take 1
```
<br>

**Answer: 152.52.146.99**<br><br>

**Q19. What protocol was this DNS query using?**<br><br>

```
NetworkFlow
| where src_ip == "10.10.16.14"
| where timestamp between (
    datetime(6/3/2025, 8:39:19 AM) .. datetime(6/3/2025, 8:59:19 AM)
)
| where dest_port == "53"
| project timestamp, src_ip, dest_ip, dest_port, protocol
| limit 10
```
<br>

**Answer: UDP**<br><br>

**Q20. What destination port was used for the HTTPS connection?**<br><br>

```
NetworkFlow
| where src_ip == "10.10.16.14"
| where dest_ip == "152.52.146.99"
| project timestamp, src_ip, dest_ip, dest_port, protocol
| take 1
```
<br>

**Answer: 443**<br><br>

**Q21. What HTTP status code was returned?**<br><br>

```
ProxyEvents
| where src_ip == "10.10.16.14"
| where domain == "docs.google.com"
| where timestamp between (datetime(2025-06-03 08:50:00) .. datetime(2025-06-03 09:00:00))
| project timestamp, src_ip, url, status_code
| take 1
```
<br>

**Answer: 200**<br><br>

**Q22. What happens first when browsing to a website: the DNS lookup or the TCP connection?**<br><br>

**Answer: DNS lookup**<br><br>

**Q23. What column contains the full URL?**<br><br>

```
ProxyEvents
| take 5
| project src_ip, url, method, status_code
```
<br>

**Answer: url**<br><br>

**Q24. What status code indicates a successful request?**<br><br>
**Answer: 200**<br><br>

**Q25. What HTTP method is used to submit form data?**<br><br>

**Answer: POST**<br><br>

**Q26. Type time to investigate to continue.**<br><br>

**Answer: time to investigate**<br><br>
