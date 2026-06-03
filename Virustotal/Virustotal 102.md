## Virustotal: Virustotal 102<br>
### **Summary**<br>
Below the Names section, there is an optional Signature Info section.
<br><br>
Developers can digitally sign files as evidence the file came from them. The signature contains a hash of the file so that if the file is modified in any way, the signature will flag as Invalid indicating that the file has been tampered with.
<br><br>
Microsoft often signs their files, but not always. As a result, the signature can be an unreliable source of truth as to if the file is from Microsoft or not.<br><br>

**Q1. To finish this question, type upload with care.**<br>

**Answer: You do you, Microsoft**<br><br>

**Q2. Does that company make sense to be providing software? To complete this question, enter the name of the first signer for the file hash.**<br><br>
Searching the hash below in Virustotal.<br><br>

```
4788925332fc6128c895b0e0736a1d7d90e3891f2abb456523cbf0c1ced7d1e2
```
<br>
Under the Details tab, then Signers, the first entry that appears is from Heart Craft Brewery s. r. o.<br><br>

**Answer: Heart Craft Brewery s. r. o**<br><br>

**Q3. But who is the first signer?**<br><br>
Under Signature info, then Signers, the first signer is shown.<br><br>

**Answer: M-Trans Maciej Caban**<br><br>

**Q4. One of the YARA rules identified that the file included encrypted content. What is the name of the rule?**<br><br>
Search for the hash below in Virustotal.<br><br>

```
a50bcbf0ef744f6b7780685cfd2f41a13be4c921d4b401384efd85c6109d7c00
```
<br>
Under the heading Crowdsourced YARA rules, the name of the ruleset that identifies encrypted content can be found.<br><br>

**Answer: INDICATOR_EXE_DotNET_Encrypted**<br><br>

**Q5. What is the popular threat label for a50bcbf0ef744f6b7780685cfd2f41a13be4c921d4b401384efd85c6109d7c00?**<br><br>

**Answer: trojan.stealer/msil**<br><br>

**Q6. According to some of the Contained in Collections groups and the comments, what threat actor used this file?**<br><br>

**Answer: JuiceLedger**<br><br>

**Q7. What malware does colinc_sophos claim this file is?**<br><br>
Searching the details for a new hash.<br><br>

```
a54ca708c3bbef76dbaec817a9bb36d8b52e492b293d2127cd5be284caabb6d1
```
<br>

**Answer: Batloader Malware**<br><br>

**Q8. What is the name of the user posting as colinc_sophos?**<br><br>
Click on username colinc_sophos, the users name will be displayed.<br><br>

**Answer: Colin Cowie**<br><br>

**Q9. According to colinc_sophos, how is this malware distributed?**<br><br>

**Answer: fake software websites & malvertizing**<br><br>

**Q10. What is the MITRE ATT&CK technique ID for this technique?**<br><br>
MITRE ATT&CK describes the technique from the last question like this:
<br><br>
"Adversaries may purchase online advertisements that can be abused to distribute malware to victims. Ads can be purchased to plant as well as favorably position artifacts in specific locations online, such as prominently placed within search engine results. These ads may make it more difficult for users to distinguish between actual search results and advertisements. Purchased ads may also target specific audiences using the advertising network’s capabilities, potentially further taking advantage of the trust inherently given to search engines and popular websites."<br><br>

This technique is known as 'Acquire Infrastructure: Malvertising'.<br><br>

**Answer: T1583.008**<br><br>

**Q11. To complete this question, provide the other file name.**<br><br>
Another SOC analyst contacted us to let us know they found yet another file with the same Certificate signer as in Question 3, but its behavior is different. This file has the file hash 0221bf1e1bd171c17527a863531518a95bcc025c87888e66b9512a5651073d16. Let's take a look at it.<br><br>

**Answer: IRS_form_Package_17-01-2023_19-25-53.exe**<br><br>

**Q12. Enter the malware family name to complete this question.**<br><br>
The first comment shows the family of the malware.<br><br>

**Answer: icedid**<br><br>

**Q13. According to the relations tab, what domain was contacted by this file?**<br><br>

**Answer: plivetrakoy.com**<br><br>

**Q14. What IP address resolved to this domain on the date closest to when the file was submitted to VirusTotal?**<br><br>

**Answer: 193.149.180.175**<br><br>

**Q15. What is the general disposition of the files? Answer with one of the following: The files look OK , Mixed Results, or All bad**<br><br>

**Answer: All bad**<br><br>

**Q16. What is the name of this file’s execution parent?**<br><br>

**Answer: IRS_form_Package_17-01-2023_19-25-53 (1).zip**<br><br>

**Q17. To complete this question, provide the SHA-1 hash for the ZIP file.**<br><br>
In the Details tab, the SHA-1 can be found.<br><br>

**Answer: 85d1e350486fea5945f46842685f248340fbf7dc**<br><br>

**Q18. What is the status of the certificate of this file?**<br><br>
Under the Signature info, Signature verification, a message shows the status of the certificate.<br><br>

```
A certificate was explicitly revoked by its issuer.
```
<br>

**Answer: revoked **<br><br>
