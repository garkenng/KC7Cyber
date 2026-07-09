## Castle & Sand: A Beachy Case of Ransomware: Section 2: Shark Attack!<br>
### **Summary**<br>
<p>
Oh no! Castle&Sand has been hit with ransomware!!! They posted a ransom note and locked all of the company's files. IT was able to get you a copy of the ransom note. Take a look at the note.
</p>


**Q1. What email address did the threat actor provide to Castle&Sand to communicate with them?**<br><br>

**Answer:  sharknadorules_gang@onionmail.org**<br><br>

**Q2. What is the unique decryption ID?**<br><br>

**Answer:  SUNNYDAY123329JA0**<br><br>

**Q3. Should this be something you post publicly about? Yes or no?**<br><br>

**Answer: No**<br><br>

**Q4. The ransom note filename was called PAY_UP_OR_SWIM_WITH_THE_FISHES.txt. How many notes appeared in Castle&Sand's environment?**<br><br>

```
FileCreationEvents
| where filename == "PAY_UP_OR_SWIM_WITH_THE_FISHES.txt"
| count 
```
<br>

**Answer: 774**<br><br>

**Q5. How many distinct hostnames had the ransom note?**<br><br>

```
FileCreationEvents
| where filename == "PAY_UP_OR_SWIM_WITH_THE_FISHES.txt"
| distinct hostname 
| count
```
<br>

**Answer: 774**<br><br>

**Q6. How many distinct employee roles were affected by the ransomware attack?**<br><br>

```
let DistinctRoles =
FileCreationEvents
| where filename == "PAY_UP_OR_SWIM_WITH_THE_FISHES.txt"
| distinct hostname;
Employees
| where hostname in (DistinctRoles)
| distinct role
```
<br>

**Answer: 18**<br><br>

**Q7. How many unique hostnames belong to IT employees?**<br><br>

```
let DistinctRoles =
FileCreationEvents
| where filename == "PAY_UP_OR_SWIM_WITH_THE_FISHES.txt"
| distinct hostname;
Employees
| where hostname in (DistinctRoles)
| where role has "IT"
| distinct hostname
```
<br>

**Answer: 25**<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

**Q.**<br><br>

**Answer: **<br><br>

