## AzureCrest - The Full Version: Section 5: Bonus: Mo' Money Mo' Problems<br>

**Q1. Enter the MITRE ATT&CK ID corresponding to this technique. Adversaries use this Execution technique to execute arbitrary code in cloud environments.**<br><br>

```
Email
| where link contains ".docm"
| distinct recipient
```
<br>

**Answer: T1648**<br><br>
