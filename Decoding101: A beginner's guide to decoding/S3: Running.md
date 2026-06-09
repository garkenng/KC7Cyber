## Decoding101: A beginner's guide to decoding: S3: Running<br>
### **Summary**<br>
Let's put into practice all you've learned so far by solving some challenges!
<br><br>

**Q1. First, can you recognise this encoding?**<br><br>

```
36 38 20 31 31 31 20 31 31 37 20 39 38 20 31 30 38 20 31 30 31 20 33 32 20 31 30 31 20 31 31 30 20 39 39 20 31 31 31 20 31 30 30 20 31 30 35 20 31 31 30 20 31 30 33 20 33 32 20 31 30 30 20 31 31 31 20 31 31 30 20 33 39 20 31 31 36 20 33 32 20 31 31 35 20 39 39 20 39 37 20 31 31 34 20 31 30 31 20 33 32 20 31 30 39 20 31 30 31 20 34 36
```
<br>

**Answer: Hex**<br><br>

**Q2. What did the previous string decode to?**<br><br>

**Answer: Double encoding don't scare me.**<br><br>

**Q3. What about this one?**<br><br>

```
MDEwMDExMTAgMDExMDExMTEgMDExMTAxMDAgMDAxMDAwMDAgMDExMDAxMDEgMDExMTAxMTAgMDExMDAxMDEgMDExMDExMTAgMDAxMDAwMDAgMDExMTAxMTEgMDExMDEwMDAgMDExMDAxMDEgMDExMDExMTAgMDAxMDAwMDAgMDExMTEwMDEgMDExMDExMTEgMDExMTAxMDEgMDAxMDAwMDAgMDExMTAxMDAgMDExMDEwMDAgMDExMTAwMTAgMDExMDExMTEgMDExMTAxMTEgMDAxMDAwMDAgMDEwMDAwMTAgMDAxMTAxMTAgMDAxMTAxMDAgMDAxMDAwMDAgMDExMDEwMDEgMDExMDExMTAgMDAxMDAwMDAgMDExMTAxMDAgMDExMDEwMDAgMDExMDAxMDEgMDAxMDAwMDAgMDExMDExMDEgMDExMDEwMDEgMDExMTEwMDAgMDAxMDAwMDE=
```
<br>

**Answer: Not even when you throw B64 in the mix!**<br><br>

**Q4. Which repeating segment was equal to 01?**<br><br>
Can do a reverse look up and use To Base64 using the value 01.<br><br>

**Answer: MDE=**<br><br>

**Q3. (typo on website) Can you manage to decode that one?**<br><br>

```
3d 3d 77 50 6c 31 47 49 79 39 6d 5a 67 49 58 5a 6b 4a 58 59 6f 42 79 5a 75 6c 47 61 30 56 57 62 76 4e 48 49 6c 5a 58 59 6f 42 53 64 76 6c 48 49 30 64 69 62 76 52 45 49 2f 55 47 62 77 6c 6d 63 30 42 53 51
```
<br>

**Answer: **<br><br>

