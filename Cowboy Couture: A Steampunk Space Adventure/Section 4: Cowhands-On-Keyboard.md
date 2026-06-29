## Cowboy Couture: A Steampunk Space Adventure: Section 4: Cowhands-On-Keyboard<br>
### Summary
You thought you had it all figured out, but this new discovery has left you confused. What does this mean? You want to reach out to Wade for help, but you remember that he's about to give his closing keynote. Frustrated, you sift through your CISSP notes, but can't find anything there to help you think through this problem.
<br><br>
Then, you remember some of the questions you answered earlier in this training module and it suddenly hits you. You know just what to do!
<br><br>

**Q1. Enter Anyone can do it! to continue**<br>
**Answer: Anyone can do it!**<br><br>

**Q2. How many succesful logins were made from that IP?**<br>

```
AuthenticationEvents
| where src_ip == "192.124.249.15" and result == "Successful Login"
| count
```
<br>

**Answer: 2**<br><br>

**Q3. What is the username for the other employee that this IP was used to log into?**<br>

```
AuthenticationEvents
| where src_ip == "192.124.249.15" and result == "Successful Login"
```
<br>

Two hostnames are returned.<br><br>

```
JHTJ-DESKTOP
ITCK-MACHINE
```
<br>
Run search for the username for hostname JHTJ-DESKTOP.<br><br>

```
Employees
| where hostname == "JHTJ-DESKTOP"
```
<br>

**Answer: jahartley**<br><br>


**Q4. What is this employee's role?**<br>
From previous query.<br><br>

**Answer: CEO**<br><br>

**Q5. Enter the timestamp for when the attacker established persisitence.**<br>
**Answer: **<br><br>


**Q. **<br>
**Answer: **<br><br>
**Q. **<br>
**Answer: **<br><br>
**Q. **<br>
**Answer: **<br><br>
**Q. **<br>
**Answer: **<br><br>
**Q. **<br>
**Answer: **<br><br>
**Q. **<br>
**Answer: **<br><br>
**Q. **<br>
**Answer: **<br><br>
