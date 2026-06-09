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

