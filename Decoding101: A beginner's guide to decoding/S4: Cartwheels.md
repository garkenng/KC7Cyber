## Decoding101: A beginner's guide to decoding: S4: Cartwheels<br>
### **Summary**<br>
This section is a bonus, to have a little bit of fun. We're going to look at CTF style cipher challenges and how to tackle them.
<br><br>
Here's the first challenge:
EEEEEEEEEeeEeEeEEEEEEEEEEeeEeEEeEEEEEEEEEeeEEEeEEEEEEEEEEeeEEEeEEEEEEEEEEeeEEEEe EEEEEEEEEeeEeeEEEEEEEEEEEeeEeeeeEEEEEEEEEeeeEeeEEEEEEEEEEeeEEeEeEEEEEEEEEeeeEEee EEEEEEEEEeeeEeEEEEEEEEEEEeeEEEEeEEEEEEEEEeeEeeEEEEEEEEEEEeeEeEeeEEEEEEEEEeeEeEEeEEEEEEEEEeeEeeeEEEEEEEEEEeeEEeee EEEEEEEEEeeeEeEEEEEEEEEEEeeEeeee EEEEEEEEEeeEEeEEEEEEEEEEEeeEeeeeEEEEEEEEEeeEeeEEEEEEEEEEEeeeEEEEEEEEEEEEEeeEeEEEEEEEEEEEEeeEeEEeEEEEEEEEEeeEeeeEEEEEEEEEEeeeEEee
<br><br>
You can feed it into CyberChef, and as you can see, the wand appears, meaning it's detected it. But refrain from clicking on it for a second, as there is another thing you should know about CyberChef: it has a Magic operation. Sometimes, even when the wand doesn't work, you can try using Magic to try and find what the possibilities are. Be aware it does not always work.
<br><br>

**Q1. What is the name of the recipe recommended by the Magic operation, as seen in its table of results?**<br><br>

**Answer: Cetacean_Cipher_Decode()**<br><br>

**Q2. What's the message?**<br><br>
Using the link to dcode.fr, paste the string below to see if it can detect what type of encoding.<br><br>

```
55 33 555 555 2 6 444 8 999 0 9 777 666 8 33 0 7777 6 7777 0 8 44 444 7777 0 9 2 999 0 666 66 222 33 0 88 7 666 66 0 2 0 8 444 6 33 0 3 666 66 8 0 6 33 66 8 444 666 66 0 444 8 0 8 666 0 8 44 33 6
```
<br>

The result is multi tap phone or T9.
<br><br>

**Answer: KELLAMITY WROTE SMS THIS WAY ONCE UPON A TIME DONT MENTION IT TO THEM**<br><br>

**Q3. What's the question you decoded?**<br><br>
Using a image reverse lookup, first result on Google was for the Aurebesh language, related to the TV series Star Trek. However this was incorrect, the image was written in Pigpen Cipher.<br><br>

**Answer: Is this really history or is it aliens**<br><br>

**Q4. What piece of useless knowledge is hidden there?**<br><br>
The string below is morse code.<br><br>

```
-- --- .-. ... . / .. ... / .- .-.. ... --- / - .... . / ..-. .-. . -. -.-. .... / .-- --- .-. -.. / ..-. --- .-. / .-- .- .-.. .-. ..- ...
```
<br>

**Answer: MORSE IS ALSO THE FRENCH WORD FOR WALRUS**<br><br>

**Q5. What is the answer, with restored spacing?**<br><br>

```
AAAAA BAAAB AABBB AAAAA ABABB AABAA BABBA ABBAB BAABB AAABA AAAAA ABBAA ABBAA ABBAB BAABA AABAA AAAAA BAABA BAABA AABBB ABAAA BAAAB ABBAB ABBAA AABAA AAAAA ABABA BAAAB ABBAB ABABA ABBAB ABBAB ABAAB BAAAB AAAAB ABAAA ABBAA AAAAA BAAAA BABBA
```
Search on decode.fr, the Bacon Cipher is detected.<br><br>

**Answer: A SHAME YOU CANNOT EAT THIS ONE ALSO LOOKS BINARY**<br><br>

**Q5. 🎉Congratulations🎉
<br><br>
You've made it to the end of this module.
<br><br>
You've learned to recognise common encoding:
<br><br>
binary
decimal
hexadecimal
base64
And also basic transformations:
reverse
ROT13
You've also seen the evil XOR.
You know they can be mixed together to make it more difficult for you to figure out.
<br><br>
You've learned how to use CyberChef, and you've practiced a bit on dcode.fr.
<br><br>
And finally, you've handled CTF-like challenges, not something useful on the day-to-day of a cybersecurity analyst, but nice to have when you want to compete for fun on your downtime ;)
<br><br>
Type I feel stronger now to finish the module.
**<br><br>
