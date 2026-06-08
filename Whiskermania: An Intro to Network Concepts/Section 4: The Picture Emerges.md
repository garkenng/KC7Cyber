## Whiskermania: An Intro to Network Concepts: Section 4: The Picture Emerges<br>
### **Summary**<br>
Morgan gets pulled away again. Something about a server issue and a volunteer who accidentally unplugged the wrong thing.
<br><br>
"Can you hold down the fort? I'll be back in an hour."
<br><br>
You're alone with the data, Jamie's notes, and Biscuits, who has curled up on the warm part of the desk near the monitor. Time to investigate properly.
<br><br>
Let's start where Jamie left off: that suspicious external IP. If anyone connected to 185.174.137.42, they had to look up the domain first. DNS will tell us what domain points to that IP.
<br><br>

**Q1. What domain resolves to 185.174.137.42?**<br><br>

```
DnsEvents
| where resolved_ips has "185.174.137.42"
| distinct query_name
```
<br>

**Answer: update-cdn-service.xyz**<br>

**Q2. How many distinct internal IPs queried this domain?**<br><br>

```
DnsEvents
| where query_name contains "update-cdn-service.xyz"
| distinct client_ip
```
<br>

**Answer: 3**<br>

**Q3. Is update-cdn-service.xyz an internal domain or an external domain?**<br>

```
DnsEvents
| where query_name contains "update-cdn-service.xyz"
| summarize count() by client_ip
| order by count_ desc
```
<br>

**Answer: external**<br>

**Q4. What destination port is this traffic using?**<br>

```
NetworkFlow
| where dest_ip == "185.174.137.42"
| project timestamp, src_ip, dest_ip, dest_port, protocol, bytes
| take 10
```
<br>

**Answer: 443**<br>

**Q5. What protocol normally runs on port 443?**<br>

**Answer: HTTPS**<br>

**Q6. What URL path appears repeatedly in these requests?**<br>

```
ProxyEvents
| where domain == "update-cdn-service.xyz"
| project timestamp, src_ip, url, method, status_code
| order by timestamp asc
```
<br>

**Answer: /api/v1**<br>

**Q7. What does C2 stand for?**<br><br>

**Answer: Command and Control**<br>
