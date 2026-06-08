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
**Answer: totally normal**<br><br>

