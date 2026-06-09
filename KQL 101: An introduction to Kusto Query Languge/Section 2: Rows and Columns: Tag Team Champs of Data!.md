## KQL 101: An introduction to Kusto Query Languge: Section 2: Rows and Columns: Tag Team Champs of Data!<br>
### **Summary**<br>
Each table is made up of columns and rows.
<br><br>
📌 Columns store specific types of information, like names, email addresses, or timestamps.
📌 Rows represent individual records in the table. Each row contains a full set of data for a single entry.
<br><br>
Knowing how tables are structured helps us ask the right questions and quickly find the answers we need.
<br><br>

**Q1. Enter row row row to continue.**<br><br>

**Answer: row row row**<br><br>

**Q2. How many rows of data did that query return?**<br><br>.

```
Employees
| take 10
```
<br>

**Answer: 10**<br><br>

**Q3. What column contains information about an employee's job title?**<br><br>
Information found from previous query.<br><br>

**Answer: role**<br><br>

**Q4. How many pharmacists work at our company?**<br><br>

```
Employees
| where role == "Pharmacist"
```
<br>

**Answer: 19**<br><br>
