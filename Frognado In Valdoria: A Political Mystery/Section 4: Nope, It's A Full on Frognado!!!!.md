## Frognado In Valdoria: A Political Mystery: Section 4: Nope, It's A Full on Frognado!!!!<br>
### **Summary**<br>
You look above the screen of your computer, checking that the creepy guy is nowhere to be seen. He’s not. Phew. You get up and run to the break room to get a cup of coffee. While the machine brews your beverage, you go over what you’ve found so far.
<br><br>
Three employees have been targeted in a seemingly internal spearphishing attack. Those attacks were successful and allowed the Shadow Truth to deface FramtidX’s website and ruin their architectural plans. Also frogs. That was the easy part.
<br><br>
The coffee machine bips. You grab your cup and walk back to your desk, pondering your next steps. You think you should investigate Alex Johnson. That employee was the source of the phishing emails. They might have been compromised themselves, or they could be an insider threat. Either way, investigating them will allow you to confirm and/or find out the entry point for the attack, but also verify if anybody else was targeted.
<br><br>
You take a sip of your coffee and start to type a new query.
<br><br>


**Q1. What is Alex Johnson’s role in the company?**<br><br>

```
Employees
| where role == "Chief Architect"
| where name !contains "Erik"
```
<br>

**Answer: Sofia Lindgren**<br><br>
