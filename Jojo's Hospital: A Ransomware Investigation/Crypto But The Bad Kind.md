## Jojo's Hospital: A Ransomware Investigation: Crypto But The Bad Kind<br>
### **Summary**<br>
JoJo's Hospital in Lexington, Kentucky, recently faced a serious cyberattack that locked their important files. The hackers sent a message to the hospital asking for money to unlock the files. They gave a specific amount of time to pay.<br><br>

**Q1. How many hours did the hackers give the hospital to pay the ransom?**<br>
Watch the YouTube video an website, approximately 41 seconds in, the states how many hours the hospital has to pay the random.

**Answer: 72**<br><br>

**Q2. What was the name of the ransomware group?**<br><br>
From the ransom note on the website, find the name of the ransomware group.<br><br>

**Answer: lock byte**<br><br>

**Q3. The slogan was: we spend your money, so ____**<br><br>
From the ransom note on the website, the slogan can be found.<br><br>

**Answer: you don't have to**<br><br>

**Q4. How much did the hackers ask the patients to pay?**<br><br>
From the ransom note on the website, the amount demanded can be found.<br><br>

**Answer: $10,000**<br><br>

**Q5. What very important unique identifier number did the ransomware operators threaten to release?**<br><br>
From the ransom note on the website list 3 categories of data, health history, medical info and social security number.
<br><br>
The most unique identifier out of the above is the social security number.<br><br>

**Answer: social security number**<br><br>

**Q6. How many total files were encrypted at the hospital?**<br><br>
Running the query from the website returns the total files that were encrypted. <br><br>

```
FileCreationEvents
| where filename endswith ".encrypted"
| count
```
<br>

**Answer: 6420**<br><br>

**Q7. How many unique hostnames had files encrypted on them?**<br><br>
Using the query given, add hostname as the distinct field and count to total the number of hostnames.<br><br>

```
FileCreationEvents
| where filename endswith ".encrypted"
| distinct hostname
| count 
```
<br>

**Answer: 321**<br><br>

