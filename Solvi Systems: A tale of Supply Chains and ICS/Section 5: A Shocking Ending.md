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

