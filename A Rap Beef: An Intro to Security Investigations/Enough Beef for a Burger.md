## A Rap Beef: An Intro to Security Investigations: Enough Beef for a Burger<br>
### **Summary**<br>
Two hip-hop artists, Dwake and Present, are in the midst of a musical feud. Following long-stewing tensions between the artists, they have begun taking jabs at each other through their music.<br>

Dwake, who is signed with OWL Records, was the first to strike. His newest song was intended to insult his arch-nemesis, Present, who is signed with Dollar Currency Records. However, he made a crucial mistake in his verse that took the feud in a different direction.
<br><br>
As a Security Analyst for OWL Records, your job is to keep the company's information safe so your artists don't get exposed during this ongoing feud.
<br><br>
**Q1 Enter ready to get started!**<br>

```
ready
```
<br>

**Q2 Type barz to continue**<br><br>
Summary of question. <br><br>
After dropping this verse, Dwake had everyone on social media talking and laughing at Present.<br><br>

Yo, Present, you don't know where I'm from,<br>
Got the Washington name from my mom's side, son.<br>
It makes sense why they call you present<br>
Cause you're so easy to beat, its pretty much a gift<br><br>

Used to play with little Fluffy, now I'm runnin' with the wolves,<br>
You say you're on top, but I'm breakin' all the rules.<br>
I'm on that next level, you're stuck in the past,<br>
with those weak beats you won't last.<br><br>
     
```
barz
```
<br>

**Q3 Type thanks dawg to continue**<br><br>
Summary of question. <br><br>

In a fit of anger, Present asked his label, Dollar Currency Records (DCR), to dig up some dirt on Dwake that he could use to retaliate.<br><br>

Your homeboy (who works in the cyber underground) gave you a tip that you might see nefarious cyber activity as a result.<br><br>

After sliding him a crisp $20 bill, he recounted a rumor he heard that DCR had hired a hacker who used the IP 18.66.52.227 to poke around your website in early April.<br><br>

```
thanks dawg
```
<br>

**Q4 What is the name of the OWL Records CEO?**<br><br>

```
Employees
| where role == "CEO"
```
<br>

**Answer: Sean Crater**<br><br>

**Q5 How many results (rows) did you get back?**<br><br>

KQl statement has been given, have to run it to see how many results it returns.<br><br>

```
InboundNetworkEvents
| where timestamp between (datetime("2024-04-10T00:00:00") .. datetime("2024-04-11T00:00:00"))
| where src_ip has "18.66.52.227"
```
<br>

**Answer: 19**<br><br>

**Q6 What piece of information were they looking to get for Dwake? (two words - might be used for communication)**<br><br>

The results from the prevoous query, under the url column we can see searches made to look for Dwake email address.<br><br>

```
https://owl-records.com/account/reset-password?username=dwaubrey&email=dwake_audrey@owl-records.com 
https://owl-records.com/search=whats+Dwake%27s+email+address%3F
```
<br>

**Answer: email address**<br><br>

**Q7 The operator is wondering why Dwake's music is so _**<br><br>
The results from query in question 5, one of the url gives the answer to the question.<br><br>

```
https://owl-records.com/search=why+is+Dwake+music+much+soo+trasshhhh
```
<br>

**Answer: trasshhhh**<br><br>

**Q8 What is Dwake's email address?**<br><br>
The results from query in question 5, the email address of Dwake is shown.<br><br>

```
https://owl-records.com/account/reset-password?username=dwaubrey&email=dwake_audrey@owl-records.com
```
<br>

**Answer: dwake_audrey@owl-records.com**<br><br>

**Q9 The operator then attempted to take over Dwake's account by resetting his password. We know this because of the reset-password parameter in that last url they accessed.<br><br>
Which of the following did Dwake disclose in his verse? (pick all that apply)**<br><br>
The results from query in question 5, under one url column it shows a password reset attempt<br><br>

```
https://owl-records.com/account/security-questions?question_1=mother's+maiden+name&answer_1=Washington&question_2=first+pet's+name&answer_2=Fluffy
```
<br>

**Answer: What is your mother's maiden name? and What is your childhood pet's name?**<br><br>

**Q10 What is Dwake's mother's maiden name?**<br><br>
Answer taken from previous url output in question 9.<br<br>

**Answer: Washington**<br><br>

**Q11 What is the name of Dwake's childhood pet?**<br><br>
Answer taken from question 9.<br<br>

**Answer: Fluffy**<br><br>

**Q12 Copy and paste the full URL that shows the operator resetting the password to Dwake’s account.**<br><br>
The code / output taken from question 9.<br><br>

**Answer: https://owl-records.com/account/security-questions question_1=mother's+maiden+name&answer_1=Washington&question_2=first+pet's+name&answer_2=Fluffy**<br><br>
