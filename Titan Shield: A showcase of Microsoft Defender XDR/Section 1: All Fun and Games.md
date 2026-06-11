## Titan Shield: A showcase of Microsoft Defender XDR: Section 1: All Fun and Games<br>
### **Summary**<br>
Welcome to TitanShield! TitanShield is a world-class defense company best known for manufacturing to keep the world safe 🦅
<br><br>
Recently, TitanShield has noticed some unusual activity on their network 🧐. But not just any network. Someone is messing with files in our most top-secret project: Project Omega! 🕵️‍♂️🖥️
<br><br>
Project Omega is TitanShield's most ambitious and classified defense project, aimed at revolutionizing modern warfare through the integration of advanced AI 🤖 and autonomous drone technology ✈️. The unified goal of Project Omega is to create an intelligent 🧠, fully autonomous defense system capable of neutralizing threats with unparalleled precision 🎯 and speed ⚡.
<br><br>
Imagine the implications if that technology got into the wrong hands!
<br><br>
Anyways… let's get to work investigating this!
<br><br>


**Q1. Enter ready to continue**<br><br>

**Answer: ready**<br><br>

**Q2. Enter LinkedIn TMI to continue**<br><br>

**Answer: LinkedIn TMI**<br><br>

**Q3. What was the name of the game that James mentioned in his LinkedIn post?**<br><br>

**Answer: DeTankWar**<br><br>

**Q4. What is James' hostname?**<br><br>

```
Employees
| where name == "James Douglas"
```
<br>

**Answer: UB9I-DESKTOP**<br><br>

**Q5. How many results did this query return?**<br><br>

```
FileCreationEvents
| where hostname == "UB9I-DESKTOP"
| where filename has "DeTankWar"
```
<br>

**Answer: 1**<br><br>

**Q6. What is the SHA256 hash of this file?**<br><br>
From prevous query.<br><br>

**Answer: 56554117d96d12bd3504ebef2a8f28e790dd1fe583c33ad58ccbf614313ead8c**<br><br>

**Q7. Enter done once you've looked it up!**<br><br>

**Answer: done**<br><br>

**Q8. What is the score assigned to this file?**<br><br>
Referring to image on website.<br><br>

**Answer: 100**<br><br>

**Q9. Which threat actor is this file attributed to?**<br><br>

**Answer: Moonstone Sleet**<br><br>

