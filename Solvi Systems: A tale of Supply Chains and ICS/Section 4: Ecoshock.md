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

**Answer: **<br><br>

