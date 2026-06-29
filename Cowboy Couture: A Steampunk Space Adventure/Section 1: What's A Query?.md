## Cowboy Couture: A Steampunk Space Adventure Section 1: What's A Query?<br>
### **Summary**<br>
Celestial Cowboy Couture, located in Deadwood, South Dakota, is on the verge of a huge breakthrough. The brand has gained increased exposure after world-famous male model John Strand starred in their latest advertising campaign. The campaign was a massive success, drawing global attention to the brand’s unique blend of cowboy and space fashion.
<br><br>
Unfortunately, this increased attention has also attracted cybercriminals eager to profit from the brand’s growth and popularity.
<br><br>
Your job is to uncover how these cybercriminals stole valuable information. By investigating the clues and analyzing the data, you can help to restore Celestial Cowboy Couture’s reputation.
<br><br>
**Q1. Enter giddy up to get started**<br>

**Answer: giddy up**<br><br>

**Q2. What is the name of the Director of Happiness?**<br><br>

```
Employees
| where role == "Director of Happiness"
```
<br>

**Answer: Jason Blanchard**<br><br>

**Q3. What is Mary Ellen Kennel's role?**<br><br>

```
Employees
| where name == "Mary Ellen Kennel"
```
<br>

**Answer: Designer**<br><br>

**Q4. What is our model's exact role?**<br><br>

```
Employees
| where role contains "model"
```
<br>

**Answer: Underwear Model**<br><br>

**Q5. What is John Strand's IP Address?**<br><br>

```
Employees
| where name == "John Strand"
```
<br>

**Answer: 10.10.0.3**<br><br>

**Q6. What is John Strand's hostname?**<br><br>
From previous query.<br><br>

**Answer: PFW2-DESKTOP**<br><br>

**Q7. What is John Strand's email address?**<br><br>
From query in question 5.<br><br>

**Answer: john_strand@celestialcowboycouture.com**<br><br>

**Q8. How many emails did John Strand receive?**<br><br>

```
Email
|where recipient == "john_strand@celestialcowboycouture.com"
| count
```
<br>

**Answer: 25**<br><br>

**Q9. How many distinct commands were run on John Strand's machine?**<br><br>

```
ProcessEvents
| where hostname == "PFW2-DESKTOP"
|distinct process_commandline
```
<br>

**Answer: 148**<br><br>

**Q10. Do a take 10 on any table and enter mosey on to continue.**<br><br>

**Answer: mosey on**<br><br>

