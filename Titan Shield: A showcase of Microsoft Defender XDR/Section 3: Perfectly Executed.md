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
