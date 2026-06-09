## Decoding101: A beginner's guide to decoding: S2: Adult Steps<br>
### **Summary**<br>
Now that you've seen the basic machine data formats, let's dive into more complex formats and other data transformations. Those are often used by threat actors to obfuscate their real intentions. Sometimes even in combination!
<br><br>
While playing KC7, you'll stumble upon such instances, so it's a good thing to be able to recognise them.
<br><br>
We will start with an easy transformation: reversing a string.
It's like if you were reading the sentence in a mirror.
<br><br>
In CyberChef, look for the Reverse operation.
<br><br>

**Q1. What does rorrim weivraer spell out?**<br><br>

**Answer: rearview mirror**<br><br>

**Q2. CyberChef prints out the amount of rotations it did by default. How many times did it do it here?**<br><br>

```
Gwc axqv um zqopb zwcvl jijg
```
<br>

**Answer: 18**<br><br>

**Q3. What is the decoded version of that string?**<br><br>

```
SSdtIGFsbCBhYm91dCB0aGF0IGJhc2UsICdib3V0IHRoYXQgYmFzZQ==
```
<br>

**Answer: I'm all about that base, 'bout that base**<br><br>

**Q4. What does it say?**<br><br>
Enter BEEF as the key in the link provided to finish the recipe.<br><br>

```
SSdtIGFsbCBhYm91dCB0aGF0IGJhc2UsICdib3V0IHRoYXQgYmFzZQ==
```
<br>

**Answer: This is XORcery x.x**<br><br>

**Q5. What is the key used here?**<br><br>
Using XOR Brute Force, search through the results for the key.<br><br>

String to brute force.<br><br>

```
W>}s{>wp>rwu{>>il{}uwpy>|rr0
```
<br>
One result is human readable.<br><br>

```
Key = 1e: I came in like a wrecking ball.
```
<br>

**Answer: 1e**<br><br>

**Q6. First, can you recognise this encoding?**<br><br>

```
36 38 20 31 31 31 20 31 31 37 20 39 38 20 31 30 38 20 31 30 31 20 33 32 20 31 30 31 20 31 31 30 20 39 39 20 31 31 31 20 31 30 30 20 31 30 35 20 31 31 30 20 31 30 33 20 33 32 20 31 30 30 20 31 31 31 20 31 31 30 20 33 39 20 31 31 36 20 33 32 20 31 31 35 20 39 39 20 39 37 20 31 31 34 20 31 30 31 20 33 32 20 31 30 39 20 31 30 31 20 34 36
```
<br>

**Answer: Hex**<br><br>


