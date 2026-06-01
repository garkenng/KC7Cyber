## CloutHaus: Social Media leads to Compromise: Got Clout<br>
### **Section 1**<br>
### **Summary**<br>
Afomiya Storm is a rising social media influencer based in Washington, D.C. 🏙️ At 25, she’s already built a strong presence in the fashion and lifestyle industry
<br><br>
Known for her relatable "Get Ready With Me" videos, "Day in My Life" vlogs, and sponsored brand collaborations, Afomiya has captured the attention of a growing audience
<br><br>
Her Instagram profile is a curated window into her life - personal, engaging, and filled with content that her followers love. She also uses her personal email for business inquiries, making it easier for potential brand partners to contact her. However, this open approach might expose her to more risks than she realizes.<br><br>

**Q1 Based on Afomiya’s Instagram profile, what is the email address she uses for brand deals?**<br>
The email address can be viewed on Afomiya’s profle page.<br><br>

**Answer: afomiya.storm@gmail.com**<br><br>

**Q2 Which of the following signs should Afomiya look for to determine if an email offering a brand deal is a phishing attempt?**<br><br>

Afomiya’s Insta fame is skyrocketing, and now her inbox is basically a runway show of brand deals ✨ Makeup brands? Check. Fitness gear? Oh, absolutely. Her feed is looking like a dream

But with all the glitter and glam comes a darker side… suddenly, her inbox is like a game of ‘Is this a legit offer or a phishing trap?’ 😱 Time to put on her detective hat and sift through the good, the bad, and the suspicious!

**Answer: E. All of the above.**<br><br>

**Q3 What technique is the threat actor using to manipulate her into revealing personal information that could compromise her email or Instagram account?**<br><br>

**Answer: Social Engineering**<br><br>

**Q4 What answer did the attacker enter to try and bypass the security questions? Enter one of the answers the attacker submitted.**<br><br>
From the screenshot, two answers were used. Kidus and Lalibela.

**Answer: Kidus or Lalibela**<br><br>

**Q5 What security measure saved Afomiya's email account from being hacked, despite the threat actor having access to her security question answers?**<br><br>

**Answer: Multifactor Authentication**<br><br>

**Q6 According to CloutHaus internal employee logs, what is Afomiya’s designated professional email?**<br><br>
Using the query below, the email address can be obtained for Afomiya.<br><br>

```
Employees
| where name contains "afomiya"
```
<br>

**Answer: afomiya_storm@clouthaus.com**<br><br>

**Q7 What is Afomiya’s role with CloutHaus?**<br><br>
The KQL query has been given. Run the query to find what role Afomiya holds.<br><br>

```
Employees
| where name contains "Afomiya"
| distinct role 
```
<br>

**Answer: Influencer Partner**<br><br>

**Q8 Based on the CloutHaus employee table, what is the status of Multi-Factor Authentication (MFA) for Afomiya’s account?**<br><br>

```
Employees
| where name contains "Afomiya"
| distinct mfa_enabled
```
<br>

**Answer: False**<br><br>

**Q9 What is the sender’s email address in the email Afomiya received from "Dior"?**<br><br>
Fill in the email address and searching for references of 'Dior' in the subject or links sent via email.<br><br>

```
Email
| where recipient == "afomiya_storm@clouthaus.com"
| where subject contains "Dior" or links contains "Dior"
```
<br>

**Answer: collabs@dior-partners.com**<br><br>

**Q10 What is the subject line of the email Afomiya received from "Dior"?**<br><br>
Answer retrieved from the previous query.<br><br>

**Answer: [EXTERNAL] Exclusive Partnership Opportunity with Dior**<br><br>

**Q11 What is the link provided in the email?**<br><br>

**Answer: ["https://super-brand-offer.com/login"]**<br><br>

**Q12 When did Afomiya click on the link? Paste the entire timestamp**<br><br>

```
OutboundNetworkEvents
| where url contains "https://super-brand-offer.com/login"
```
<br>

**Answer: 4/3/2025, 11:20:00 AM**<br><br>

**Q13 What username did she enter?**<br><br>
The second result from the previous query shows the username used.<br><br>

**Answer: afstorm**<br><br>

**Q14 What is the IP address associated with the domain?**<br><br>

```
PassiveDns
| where domain contains "super-brand-offer.com"
```
<br>

**Answer: 198.51.100.12**<br><br>

**Q15 How many distinct domains are linked to the suspicious IP address?**<br><br>

```
PassiveDns
| where ip contains "198.51.100.12"
| distinct domain
```
<br>

**Answer: 3**<br><br>

**Q16 Enter: I have MFA setup for my Instagram!**<br><br>

**Answer: I have MFA setup for my Instagram!**<br><br>

**Q17 What are the followers really investing in: a great deal or a phishing scam?**<br><br>

**Answer: phishing scam**<br><br>

**Q18 Based on the images showing the apartment view and amenities from Afomiya’s Instagram post, use a reverse image search to identify the name of the apartment building.**<br><br>

**Answer: City Center Apartments**<br><br>

**Q19 ENTER: Unlocking trouble with a photo!**<br><br>

**Answer:  Unlocking trouble with a photo!**<br><br>

**Q20 What should you never reuse across different sites to protect your accounts?**<br><br>

**Answer: Passwords**<br><br>

**Q21 ENTER: Be the hunter, not the hunted!**<br><br>

**Answer: Be the hunter, not the hunted!**<br><br>
