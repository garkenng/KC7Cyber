## KQL 101: An introduction to Kusto Query Languge: Section 3: Commands and Operators: The Finishing Moves<br>
### **Summary**<br>
In KQL, we use commands and operators to explore and filter data. Let’s start with a key command called take.
<br><br>
take grabs a small number of rows to preview data. It’s a useful way to quickly see what’s inside a table without running a large query.
<br><br>
We build our queries by starting with the Table name. On the next line, we use a | (pipe) followed by our command. The cool thing about KQL is that it will often autofill suggestions as you type.
<br><br>
Let’s try it!
<br><br>

**Q1. Do a take 10 on a table of your choice and enter when in doubt take 10.**<br><br>

**Answer: when in doubt take 10**<br><br>

**Q2. How many employees work at our company?**<br><br>

```
Employees
| count
```
<br>

**Answer: 321**<br><br>

**Q3. How many distinct employee roles do we have at our company?**<br><br>

```
Employees
| distinct role
| count 
```
<br>

**Answer: 23**<br><br>

**Q4. How many Radiologists with the name Richard do we have at our company?**<br><br>

```
Employees
| where name contains "Richard"
| where role == "Radiologist"
```
<br>

**Answer: 2**<br><br>

**Q5. What is Noemi's email address?**<br><br>

```
Employees
| where name == "Noemi Tep"
```
<br>

**Answer: noemi_tep@jojoshospital.org**<br><br>

**Q6. What is the name of the exact role?**<br><br>

```
Employees
| where role contains "security"

```
<br>

**Answer: Security Officer**<br><br>

**Q7. How many emails did we receive that have the word health in the subject?**<br><br>

```
Email
| where subject has "health"
| count
```
<br>

**Answer: 613**<br><br>

**Q8. Who is the sender for the last external email received by Noemi?**<br><br>

```
Email
| where recipient == "noemi_tep@jojoshospital.org"
| where sender !contains "jojoshospital"
```
<br>

**Answer: skirmishes.converts@yandex.com**<br><br>

**Q9. How many failed login attempts were there from this IP address?**<br><br>

```
AuthenticationEvents
| where src_ip == "10.10.0.144" and result == "Failed Login"
```
<br>

**Answer: 59**<br><br>

**Q10. How many results do we get in AuthenticationEvents for these two IP addresses?**<br><br>

```
AuthenticationEvents
| where src_ip == "10.10.0.144" or src_ip == "10.10.0.86"
| count
```
<br>

**Answer: 131**<br><br>

**Q11. How many failed login attempts were from these IP addresses?**<br><br>

```
AuthenticationEvents
| where src_ip in ("10.10.0.144", "10.10.0.86", "10.10.0.86", "10.10.0.20", "10.10.0.109") and result == "Failed Login"
| count 
```
<br>

**Answer: 169**<br><br>
