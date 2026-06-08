## Solvi Systems: A tale of Supply Chains and ICS: Section 5: A Shocking Ending<br>
### **Summary**<br>
Looks like we hit a dead end. The threat actors didn't seem interested enough to do anything else on Carla's machine.
<br><br>
We can use this as an anchor point though. Perhaps the threat actor is a creature of habit.
<br><br>
Good news: we have new leads in our investigation. Bad news: we have more investigating to do! Let's explore these malicious emails that were sent by the adversary.
<br><br>

**Q1. How many distinct commands containing the term net use were run on SolviSystem devices?**<br><br>

```
ProcessEvents
| where process_commandline contains "net use"
| distinct process_commandline
```
<br>
Results returned are:<br><br>

```
net users /add gu@rd!an abc1toothree
net use
net use /PERSISTENT:YES
```
<br>
3 results are returned, but only 2 have commands.<br><br>

**Answer: 2**<br><br>

**Q2. What new command using net use did we find?**<br><br>
From previous query, a new command is shownn.<br><br>

**Answer: net use /PERSISTENT:YES**<br><br>

**Q3. How many distinct hosts was this command run on?**<br><br>

```
ProcessEvents
| where process_commandline == "net use /PERSISTENT:YES"
| distinct hostname
| count
```
<br>

**Answer: 3**<br><br>

**Q4. What is the timestamp for the first time this command was run?**<br><br>

```
ProcessEvents
| where process_commandline == "net use /PERSISTENT:YES"
```
<br>

**Answer: 5/27/2024, 4:23:10 PM**<br><br>

**Q5. What is the hostname from that timestamp?**<br><br>
Obtained from previous query.<br><br>

**Answer: SJ9V-MACHINE**<br><br>

**Q6. Who is the employee associated with that hostname?**<br><br>

**Answer: **<br><br>


