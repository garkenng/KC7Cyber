## Frognado In Valdoria: A Political Mystery: Section 2: KQL 101<br>
### **Summary**<br>
Welcome to the next phase of your investigation in Valdoria!
<br><br>
You’ve made impressive progress uncovering the layers of this mystery, but now it’s time to dive deeper. To do that, you’ll need to leverage the power of KQL (Kusto Query Language) to sift through the data and find the evidence.
<br><br>
Your first stop is to meet with Kell, a security analyst at FramtidX Development Corp. They’re known for their expertise in KQL and have been eagerly awaiting your arrival.
<br><br>
Kell greets you with a friendly smile and leads you to their workstation. “KQL is like a detective’s magnifying glass,” they say. “It helps you see the fine details hidden in the data.”
<br><br>
Ready to become a KQL detective and continue the investigation?
<br><br>

**Q1. Type let’s do this to begin your KQL training.**<br><br>

**Answer: let's do this**<br><br>

**Q2. Once you've looked at all the tables type when in doubt take 10 to continue.**<br><br>

**Answer: when in doubt take 10**<br><br>

**Q3. How many employees work at FramtidX?**<br><br>

```
Employees
| count
```
<br>

**Answer: 755**<br><br>

**Q4. What is the CEO’s name?**<br><br>

```
Employees
| where role == "CEO"
```
<br>

**Answer: Johanna Karlsson**<br><br>

**Q5. Enter operator, operator to continue.**<br><br>

**Answer: operator, operator**<br><br>


**Q6. How many emails did Mona Hunter receive?**<br><br>

```
let MonaEmails = 
    Employees
    | where name == "Mona Hunter"
    | distinct email_addr;
Email
| where recipient in (MonaEmails)
| count
```
<br>

**Answer: 24**<br><br>


**Q7. How many distinct senders were seen in the email logs from techinnovators.io?**<br><br>

```
Email
| where sender has "techinnovators.io"
| distinct sender
| count
```
<br>

**Answer: 675**<br><br>

**Q8. How many distinct websites did Mona Hunter visit?**<br><br>

```
let MonaIP = 
    Employees  
    | where name == "Mona Hunter"
    | distinct ip_addr;
OutboundNetworkEvents
| where src_ip in (MonaIP)
| distinct url
| count
```
<br>

**Answer: 46**<br><br>


**Q9. How many distinct domains in the PassiveDns records contain the word green?**<br><br>

```
PassiveDns
| where domain contains "green"
| distinct domain
| count 
```
<br>

**Answer: 11**<br><br>


**Q10. How many distinct URLs did employees with the first name Dorothy visit?**<br><br>

```
let dorothy_ips =   
    Employees
    | where name has "Dorothy"
    | distinct ip_addr;
OutboundNetworkEvents
| where src_ip in (dorothy_ips)
| distinct url
| count 
```
<br>

**Answer: 419**<br><br>

**Q11. How many authentication attempts did we see to the accounts of employees with the first name Dorothy?**<br><br>

```
let dorothy_ips =   
    Employees
    | where name contains "Dorothy"
    | distinct username;
AuthenticationEvents
| where username  in (dorothy_ips)
```
<br>

**Answer: 490**<br><br>

**Q12. Type ready for more to continue to the next part of the investigation.**<br><br>

**Answer: ready for more**<br><br>
