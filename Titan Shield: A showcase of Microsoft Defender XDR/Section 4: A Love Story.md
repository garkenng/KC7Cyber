## Titan Shield: A showcase of Microsoft Defender XDR: Section 4: A Love Story<br>
### **Summary**<br>
Now that we've identified how the attackers got in (phishing email), we need to figure out what they did once they got here.
<br><br>
The threat intelligence article mentions two malicious DLLs that may be included with the tank game: NVUnityPlugin.dll or Unityplayer.dll.
<br><br>
Don't have access to Defender XDR? Click here for a screenshot
<br><br>
Let's query our logs to see if either of those files show up in our environment.
<br><br>


**Q1. What is chtaylor's hostname?**<br><br>

```
Employees
| where username == "chtaylor"
```
<br>

**Answer: IL5M-DESKTOP**<br><br>

**Q2. When was this process executed on Taylor's machine? (Copy and paste the exact time.)**<br><br>

```
ProcessEvents
| where hostname == "IL5M-DESKTOP"
| where process_commandline has "whoami"
```
<br>

**Answer: 7/20/2024, 3:58:19 AM**<br><br>

**Q3. What was the exact process that was executed?**<br><br>
From previous query.<br><br>

**Answer: cmd.exe /c echo PC and User Names -------- >>%temp%\Logs.txt && whoami >>%temp%\Logs.txt**<br><br>

**Q4. How many similar processes do we find on Taylor's machine?**<br><br>

```
ProcessEvents
| where hostname == "IL5M-DESKTOP"
| where process_commandline has_all("echo", ">>", "logs.txt")
```
<br>

**Answer: 39**<br><br>


**Q5. What is the path, including the filename, where these commands are being dumped?**<br><br>
From previous query.<br><br>

```
cmd.exe /c echo Date and Time -------- >>%temp%\Logs.txt && date /t >>%temp%\Logs.txt && time /t >>%temp%\Logs.txt
```
<br>

**Answer: %temp%\Logs.txt**<br><br>


**Q6. Which domain is this?**<br><br>

**Answer: yandex.com**<br><br>


**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
**Q. **<br><br>

**Answer: ready**<br><br>
