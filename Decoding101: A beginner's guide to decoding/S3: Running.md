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
From HEX<br><bR>

```
==wPl1GIy9mZgIXZkJXYoByZulGa0VWbvNHIlZXYoBSdvlHI0dibvREI/UGbwlmc0BSQ
```
<br>
Then Reverse the string.<br><br>

```
QSB0cmlwbGU/IERvbid0IHlvdSBoYXZlIHNvbWV0aGluZyBoYXJkZXIgZm9yIG1lPw==
```
<br>
Then From Base64.<br><br>

**Answer: A triple? Don't you have something harder for me?**<br><br>

**Q4. (typo on website) That one is a bit trickier, no?**<br><br>

```
48 49 49 49 48 49 48 48 32 49 48 48 48 49 49 49 48 32 48 49 48 48 49 49 49 48 32 49 48 49 48 48 49 49 48 32 48 49 49 49 48 49 49 48 32 48 48 48 48 49 49 49 48 32 48 49 49 48 48 49 49 48 32 48 48 48 48 48 49 48 48 32 49 49 49 48 48 49 49 48 32 49 49 49 48 48 49 48 48 32 49 48 48 48 48 49 49 48 32 48 49 49 48 49 49 49 48 32 48 49 49 49 48 49 49 48 32 48 48 48 48 48 49 48 48 32 48 49 49 48 49 48 49 48 32 48 48 48 48 48 49 48 48 32 48 48 49 49 48 49 48 48 32 49 49 49 48 48 49 49 48 32 49 48 48 48 48 49 49 48 32 48 49 49 49 48 49 49 48 32 48 49 48 49 48 49 49 48 32 48 48 48 48 48 49 48 48 32 48 48 48 49 48 49 49 48 32 48 49 48 48 48 49 49 48 32 48 48 49 49 48 49 49 48 32 48 48 48 48 48 49 48 48 32 48 49 49 48 48 49 49 48 32 48 49 49 49 48 49 49 48 32 48 48 48 48 48 49 48 48 32 48 49 49 48 48 49 49 48 32 49 49 48 48 48 49 49 48 32 48 49 48 48 49 49 49 48 32 49 49 49 48 48 49 49 48 32 48 49 49 48 48 49 49 48 32 48 48 48 48 48 49 48 48 32 48 48 49 49 48 49 49 48 32 49 48 48 48 48 49 49 48 32 48 49 49 49 48 49 49 48 32 48 49 48 49 49 49 49 48 32 48 48 48 48 48 49 48 48 32 48 49 49 48 48 49 49 48 32 48 49 49 49 48 49 49 48 32 48 48 48 48 48 49 48 48 32 49 48 48 48 49 49 49 48 32 49 48 48 48 49 49 49 48 32 48 49 49 49 48 49 49 48 32 48 48 48 48 48 49 48 48 32 49 48 48 48 48 49 49 48 32 48 49 49 49 48 49 49 48 32 48 48 48 48 49 49 49 48 32 48 48 48 48 48 49 48 48 32 48 48 48 49 48 49 49 48 32 48 49 48 48 48 49 49 48 32 48 48 49 49 48 48 49 48
```
<br>
Above encoded 4 times. Decimal - Reverse - Binary - ROT13.<br><br>

**Answer: You can add as many steps as you want, I ain't scared.**<br><br>

**Q5. What is the payload message?**<br><br>

```
#Obfuscated payload
$key = 0x8F
$payload = "jbe+q/6+m3+ru/K/uj/rqHO4vyv5nv/r8zv66j+rG/65uru9"

# Decode
$s1 = -join ($payload.ToCharArray()[-1..-($payload.Length)])
$s2 = [System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($s1))
$msg = -join ($s2.ToCharArray() | ForEach-Object { [char]([byte][char]$_ -bxor $key) })

# Execute
Write-Host $msg

# Cleanup traces
Remove-Item $MyInvocation.MyCommand.Path -Force -ErrorAction SilentlyContinue
```
<br>

**Answer:**<br><br>

