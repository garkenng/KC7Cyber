## A Scandal in Valdoria: A Political Mystery<br>
### **Summary**<br>
The Valdorian Times has hired you as a cyber incident responder to help investigate the incident and get to the bottom of how the falsified article was published. The full background to the investigation can be found below.<br><br>

**Q1**<br>
**Enter ready to get started!**<br>

```
ready
```
<br>
To start the investigation, I will be using the Azure Data Explorer (ADX) which contains top secret data from The Valdorian Times.<br><br>

**Q2**<br>
**Type done to earn credit for this question.**<br>

```
done
```
<br>

**Q3**<br><br>

**How many employees work at the Valdorian Times?**<br>

```
Employees
| count
```
<br>

**Answer: 100**
<br><br>

**Q4**<br><br>
**What is the Editorial Director's name?**<br>

```
Employees
| where role == "Editorial Director"
```
<br>
**Answer: Nene Leaks.**
<br><br>
From the previous inquiry, we can retrieve Nene Leaks email address: nene_leaks@valdoriantimes.news.<br><br>

**Q5**<br><br>
**How many emails did Nene Leaks receive?**<br>

```
Email
| where recipient == "nene_leaks@valdoriantimes.news"
| count
```
<br>
**Answer: 18.**
<br><br>

**Q6**<br><br>
**How many distinct senders were seen in the email logs from the domain name "weprinturstuff.com"?**<br><br>
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

**Q7**<br><br>
**How many distinct URLs did “Lois Lane” visit?**<br><br>
