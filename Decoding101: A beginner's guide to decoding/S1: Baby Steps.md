## Decoding101: A beginner's guide to decoding: S1 Baby Steps<br>
### **Summary**<br>
Welcome to Decoding101, the module in which we'll learn to turn what looks like gibberish into perfectly normal words 🤓
<br><br>
Why is this skill useful?
<br><br>
- Data can be formatted in a way that is easier to understand by machines, and way less by humans. Knowing how those formats look like will save you lots of headaches when trying to convert it back to something you can read.
- Threat actors will try to bypass a network's defenses by encoding their malicious commands, making them harder to detect. Being able to recognise those encodings will help you find them and translate them to understand what they're doing during your investigation.
- CTFs often have challenges in which you must decode/decrypt a hidden message. You might not always be able to recognise the encoding/cyber used by yourself, but knowing which tools can help in those tasks will save you from throwing your computer out the window (money saved!).
Before you start worrying, no, you do not need to have any coding skills. There are handy tools that will do all the "translation" work for you, and even the "recognition" work. The most popular is CyberChef, a free web app that you will learn to use here.
<br><br>
Let's dive in, shall we? 🤿
<br><br>

**Q0. Type future secret master to start your learning journey!**<br><br>

**Answer: future secret master**<br><br>

**Q1. Which symbol is used as an example in the "Url Decode" operation?**<br><br>
Hover the mouse over URL Decode an example pop up appears and shows the following:
<br><br>
Converts URI/URL percent-encoded characters back to their raw values.
<br><br>
e.g. %3d becomes =
<br><br>
Percent-encodingopen_in_new on Wikipedia
<br><br>

**Answer: =**<br><br>

**Q2. What does this binary string say?**<br><br>
Select From Binary in Operations window and drag to Recipe column. <br><br>

```
01100010 01100101 01100101 01110000 00100000 01100010 01101111 01101111 01110000 00100000 01110100 01101000 01101001 01110011 00100000 01101001 01110011 00100000 01100010 01101001 01101110 01100001 01110010 01111001 00101110
```
<br>

**Answer: beep boop this is binary.**<br><br>

**Q3. What does the decimal encoded string says?**<br><br>
Select From Decimal in Operations window and drag to Recipe column. <br><br>

```
73 32 104 97 116 101 32 109 97 116 104 115 32 232 45 233
```
<br>

**Answer: I hate maths è-é**<br><br>

**Q4. What is the decoded message?**<br><br>
Select From Hex in Operations window and drag to Recipe column. <br><br>
```
4f 68 20 6e 6f 21 20 59 6f 75 27 76 65 20 62 65 65 6e 20 68 65 78 65 64 21
```
<br>

**Answer: Oh no! You've been hexed!**<br><br>

**Q5. What recipe was used?**<br><br>
Pasting the below and selecting the magic wand will auto detect the encoding.<br><br>

```
00110101 00110000 00100000 00110111 00110101 00100000 00110111 00110010 00100000 00110110 00110101 00100000 00110010 00110000 00100000 00110110 01100100 00100000 00110110 00110001 00100000 00110110 00110111 00100000 00110110 00111001 00100000 00110110 00110011 00100000 00110010 00110001
```
<br>

**Answer: from binary from hex**<br><br>
