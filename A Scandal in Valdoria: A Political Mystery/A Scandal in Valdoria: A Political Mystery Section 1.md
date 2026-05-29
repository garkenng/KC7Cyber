## A Scandal in Valdoria: A Political Mystery<br>
### **Section 1**<br>
### **Summary**<br>
The Valdorian Times has hired you as a cyber incident responder to help investigate the incident and get to the bottom of how the falsified article was published. The full background to the investigation can be found below.<br><br>

**Q1 Enter ready to get started!**<br>

```
ready
```
<br>
To start the investigation, I will be using the Azure Data Explorer (ADX) which contains top secret data from The Valdorian Times.<br><br>

**Q2 Type done to earn credit for this question.**<br>

```
done
```
<br>

**Q3 How many employees work at the Valdorian Times?**<br>

```
Employees
| count
```
<br>

**Answer: 100**
<br><br>

**Q4 What is the Editorial Director's name?**<br>

```
Employees
| where role == "Editorial Director"
```
<br>

**Answer: Nene Leaks.**
<br><br>
From the previous inquiry, we can retrieve Nene Leaks email address: nene_leaks@valdoriantimes.news.<br><br>

**Q5 How many emails did Nene Leaks receive?**<br>

```
Email
| where recipient == "nene_leaks@valdoriantimes.news"
| count
```
<br>

**Answer: 18.**
<br><br>

**Q6 How many distinct senders were seen in the email logs from the domain name "weprinturstuff.com"?**<br><br>
First we need to look at the schema for the Email table to determine what column we can use to search for distinct senders.

```
Email
| take 10
```
<br>

The query returned the columns.

- timestamp 
- sender
- reply_to
- receipient
- subject
- verdict
- link

The 'sender' column along with the doman name given in the question to run the next query.<br><br>

```
Email
| where sender has "weprinturstuff.com"
| distinct sender
| count
```

**Answer: 100**.
<br><br>

**Q7 How many distinct URLs did “Lois Lane” visit?**<br><br>
We have been given the table to pull the answer from, OutboundNetworkEvents. Lets inspect the schema of this table.<br><br>

```
OutboundNetworkEvents
| take 10
```
<br>

The query returned the columns.

- timestamp 
- method
- src_ip
- user_agent
- url

<br>
Need to determine what IP address Lois Lane is using. From the Employees table, need to determine if there is a column we can pull this information from.

```
Employees
| take 10
```
<br>

The query returned the columns.

- hire_date 
- name
- user_agent
- ip_addr
- email_addr
- company_domain
- username
- role
- hostname

<br>

Can search using name 'Lois Lane' and it will return the column ip_addr which is the IP address (src_ip) we need to search the OutboundNetworkEvents table.

```
Employees
| where name == "Lois Lane"
```
<br>
Result: ip_addr = 10.10.0.22.
<br><br>
Passing the ip_addr to the OutboundNetworkEvents table. <br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.22"
| distinct url
| count
```
<br>

**Answer: 62**

<br><br>
**Q8 How many distinct domains in the PassiveDns records contain the word “hire”?**<br><br>
Viewing the schema for the PassiveDns table.<br><br>

```
PassiveDns
| take 10
```
<br>

The query returned the columns.

- timestamp 
- ip
- domain

Can search under the domain column for the word "hire".

``` 
PassiveDns
| where domain contains "hire"
| distinct domain
| count 
```
<br>

**Answer: 6**<br><br>

**Q9 What IPs did the domain “jobhire.org” resolve to (enter any one of them)?**<br><br>

```
PassiveDns
| where domain == "jobhire.org"
| distinct ip
```
<br>

**Answer: 191.7.248.112**<br><br>

**Q10 How many distinct websites did employees with the first name "Mary" Visit?**<br><br>
The site introduces the let statement. Which is essentially storing the result of a query into a variable. The KQL has been given to use, just need to fill in the "Employee Name" which is Mary and Count to return the number of records in the table OutboundNetworkEvents with Marys IP address.<br><br>

```
let mary_ips = 
Employees
| where name has "Mary"
| distinct ip_addr;
OutboundNetworkEvents
| where src_ip in (mary_ips)
| count
```
<br>

**Answer: 58**<br><br>

**Q11 How many authentication attempts did we see to the accounts of employees with the first name Mary?**<br><br>
The KQL has been given. Need to fill in the blanks. First is to rename the let statement to 'attempts', then add Mary as the Employee Name.<br><br>

```
let attempts = Employees
| where name has "Mary"
| distinct username;
AuthenticationEvents
| where username in (attempts)
| count
```
<br>

**Answer: 70**

This is the end of section 1 and greeted with the message<br><br>

```
Congratulations! 🥳 You've passed KQL 101! Let's dive into the investigation! 🔎

Enter ready to earn credit for this question.
```
<br>

```
ready
```
<br>
Moving onto section 2.
