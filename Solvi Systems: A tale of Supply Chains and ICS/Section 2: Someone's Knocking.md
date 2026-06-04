## Solvi Systems: A tale of Supply Chains and ICS: Section 2: Someone's Knocking<br>
### **Summary**<br>
Our mission is to identify any intrusion attempts against Solvi Systems. In order to do this, we'll start by reviewing some alerts.
<br><br>
You got an alert from your Web Application Firewall (WAF) appliance that someone may be trying to compromise your Solvi System's website!<br><br>

**Q1. What kind of attack does the alert suggest happened?**<br><br>

```
{
   description: "DETECTION RULE TRIGGERED",
   severity: "HIGH",
   rule_description: "SUSPICIOUS TEXT IN HTTP REQUEST",
   data: https://www.solvisystems.com/feedback?message=</script>. 
 <script>alert('xss')</script>
}

```
<br>

Based on the above alert, the attack is XSS / Cross Site Scripting.<br><br>

**Answer: xss**<br><br>

**Q2. What javascript command was the attacker trying to run?**<br><br>

```
InboundNetworkEvents
| where url contains "alert"
```
<br>
From the url column, the following data is shown.<br><br>

```
https://www.solvisystems.com/feedback%3Fmessage%3D%3C/script%3E%3Cscript%3Ealert%28%27xss%27%29%3C/script%3E
```
<br>

**Answer: alert**<br><br>

**Q3. What response code did they receive from the website?**<br><br>
Response code from previous query.<br><br>

**Answer: 404**<br><br>

**Q4. What user agent did the attackers use to make the web requests in this attack? Enter only the initial part of the user agent (XXXXX/N.NN).**<br><br>
Under the user agent column from query in question 2, the user agent can be found.<br><br>

```
Opera/8.64.(X11; Linux x86_64; kok-IN) Presto/2.9.165 Version/10.00
```
<br>

**Answer: Opera/8.64**<br><br>

**Q5. On what day did the attack happen? Give the timestamp in the format YYYY-MM-DD.**<br><br>
The timestamp from the query in question 2 is.

```
5/3/2024, 2:48:08 PM
```
<br>

**Answer: 2024-05-03**<br><br>

**Q6. How many malicious requests did the attacker make in total?**<br><br>
The full user agent information pulled from query in question 2.<br><br>

```
InboundNetworkEvents
| where user_agent == "Opera/8.64.(X11; Linux x86_64; kok-IN) Presto/2.9.165 Version/10.00"
| where timestamp between (datetime("2024-05-03") .. datetime("2024-05-05"))
```
<br>

**Answer: 9**<br><br>

**Q7. Were any of these attacks successful? (yes/no)**<br><br>
No attacks were successful as all the response code from the malicious requests returned a 404 Not Found.<br><br>

**Answer: no**<br><br>

**Q8. What IP addresses did the requests originate from? (Enter any of them.)**<br><br>
Taking first result from query in question 6.<br><br>

**Answer: 98.117.26.236**<br><br>

**Q9. How many total records do we have of them browsing Solvi Systems?**<br><br>

```
InboundNetworkEvents
| where user_agent == "Opera/8.64.(X11; Linux x86_64; kok-IN) Presto/2.9.165 Version/10.00"
```
<br>


**Answer: 64**<br><br>

**Q10. What is the timestamp of the first web request the threat actor sent to Solvi System's website?**<br><br>
The first result that came through from the previous query is.**<br><br>

```
5/1/2024, 12:00:00 AM
```
<br>

**Answer: 5/1/2024, 12:00:00 AM**<br><br>

**Q11. Which product did the threat actors research before the day that they sent the malicious web requests?**<br><br>
Searching throughthe urls, searches made for product called docks-ics.<br><br>

```
https://www.solvisystems.com/products/docks-ics/features
```
<br>

**Answer: docks-ics**<br><br>

**Q12. How many distinct domains do the ip addresses used by the threat actor resolve to?**<br><br>
Using all the IP addresses at are associated with the malicious attacker.<br><br>

```
PassiveDns
| where ip == "13.201.46.208"  or ip == "105.78.23.64" or ip == "56.6.30.190" or ip == "105.78.23.64" or ip == "98.117.26.236"
| distinct domain
```
<br>

**Answer: 3**<br><br>

**Q13. Did we receive any emails containing these domains? (yes/no)**<br><br>

```
Email
| where link contains "eco-awareness-update.net" or link contains "news-on-industry.com" or link contains "energy-trends4u.net"
```
<br>
Since results are produced containing the malicious domains, then emails were received by employees.<br><br>

**Answer: yes**<br><br>

