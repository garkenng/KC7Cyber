## Solvi Systems: A tale of Supply Chains and ICS: Section 4: Ecoshock <br>

**Q1. How many records do we have of this file being created on Solvi Systems computers?**<br><br>

```
FileCreationEvents
| where filename contains "ecobug.exe"
```
<br>

**Answer: 39**<br><br>

**Q2. What IP address does ecobug.exe connect to in order to establish persistence?**<br><br>

```
ProcessEvents
| where process_commandline contains "ecobug.exe"
```
<br>
A result from the process command line column shows the IP addressed used to establish persistence.<br><br>

```
ecobug.exe --timeout 6000 --dest 98.117.26.236 --port 1337
```
<br>

**Answer: 98.117.26.236**<br><br>

**Q3. What is the port number that is used?**<br><br>
From previous query, port number can be found.<br><br>

**Answer: 1337**<br><br>

**Q4. How many times does Carla's machine connect to the suspicious IP address?**<br><br>

```
NetworkFlow
| where src_ip == "10.10.0.164" // Carla's IP address
| where dest_ip == "98.117.26.236" // Suspicious IP address
```
<br>

**Answer: 24**<br><br>

**Q5. How many times a day does Carla's machine make its recurring connection to the suspicious IP?
Looking at the timestamps from the query. Carla machine makes one connection per day at the exact same time.<br><br>

```
5/1/2024, 5:38:25 PM
5/2/2024, 5:38:25 PM
5/3/2024, 5:38:25 PM
```
<br>

**Answer: 1**<br><br>

**Q6. At what time does this connection take place? (format hh:mm:ss)**<br><br>
Obtain answer from previous question.<br><br>

**Answer: 5:38:25 PM**<br><br>

**Q7. How many total connections do we see between this IP and Solvi Systems employee machines?**<br><br>

```
NetworkFlow
| where dest_ip == "98.117.26.236"
| count
```
<br>

**Answer: 470**<br><br>



**Q8. How many distinct employee machines are involved in those connections?**<br><br>

```
NetworkFlow
| where dest_ip == "98.117.26.236"
| distinct src_ip
| count
```
<br>

**Answer: 38**<br><br>

**Q9. We've gained some pretty good information on how the malware communicated with the threat actor's infrastructure. Let's go back to the malware to see what actions it performed on the victims' machines.
<br><br>
A day after the malware is first executed the threat actor attempts to create a new user and add that user to the local administrators group.
<br><br>
What is the name of the newly created user?**<br><br>

A day after the malware was click would be 5/2/2024 at 5:38 PM. Search for events on the process command line that references anything to do with creating a new usser.<br><br>

```
ProcessEvents
| where timestamp >= datetime(5/2/2024, 5:38 PM)
| where process_commandline contains "user"
```
<br>
The first result returned is.<br><Br
                                   
```
net users /add gu@rd!an abc1toothree
```
<br>

The command above is to add a new user with a specified username and password.<br>

**Answer: gu@rd!an**<br><br>

**Q10. What is that user's password?**<br><br>
Retrieved from previous question.<br><br>

**Answer: abc1toothree**<br><br>

**Q11. What was the last discovery command that the adversaries ran?**<br><br>

```
ProcessEvents
| where timestamp >= datetime(5/2/2024, 5:38 PM)
| where username == "cawharton"
```
The first result that comes back from the query is the last discovery command the adversaries ran.<br><br>

**Answer: net use**<br><br>
