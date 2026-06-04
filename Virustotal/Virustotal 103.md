## Virustotal: Virustotal 103<br>
### **Summary**<br>
While we were working, our Threat Intel team informed us they found yet another file with the same certificate signer! The Intel team informs us that criminals impersonate companies to get certificates and then sell the certificates to sign the malware for multiple malware developers!
<br><br>
The hash of the file is 2bf0a64fe7aea262c96fc7d52b1e28486ff607caa9513fd88583e19454f9c500.
<br><br>

**Q1. What is the status of the certificate of this file?**<br><br>
Under the Signature info, Signature verification, a message shows the status of the certificate.<br><br>

**Answer: revoked**<br><br>

**Q2. What is the Creation Time for this file?**<br><br>

**Answer: 1992-06-19 22:22:17 UTC**<br><br>

**Q3. What is the name of the compiler of this file?**<br><br>
The compiler can be found on the Basic properties section, next to DetectItEasy.<br><br>

**Answer: Borland Delphi**<br><br>

**Q4. What is the name of the DLL file which was observed connecting to this IP address on 2025-02-12?**<br><br>
In the Relations tab, Graph Summary, clicked on the link for '9 communicating files'. Looking through the communicating files, 'PEDLL', there are two Win32 DLL files. Can see it connected to the C2 IP: 146.70.161.126, however unable to confirm the date.<br><br>

**Answer: WABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZoYDHNFTTPDJL50NWXNEWCHBUDCPJOeEZNbd**<br><br>

**Q5. What is the file's size?**<br><br>
Under the Details tab, the File Size is shown.<br><br>

**Answer: 301.35 MB**<br><br>

**Q6. What is the size of the deflated file?**<br><br>
From the Yomi Hunter sandbox report, the file size can be obtained.<br><br>

**Answer: 2.52 MB**<br><br>

**Q7. To complete this question, provide the full filepath. (Note: leave the filename off as it may change if this file is re-analyzed.)**<br><br>
Under the File system actions, Files Written, searching through the file paths with a lnk file.<br><br>

**Answer: %APPDATA%\microsoft\windows\start menu\programs\startup** **\\** <br><br>

**Q8. What is the full name of the registry hive?**<br><br>

**Answer: HKEY_CURRENT_USER**<br><br>

**Q9. What program will the registry key execute when called? This is the first word written to the registry key.**<br><br>
Under the Registry Keys Set, there are 4 paths which have shell\open\command. Expanding the first one shows that the application powershell is executed.<br><br>

**Answer: powershell**<br><br>

**Q10. What type of encryption algorithm is mentioned and used by the registry key?**<br><br>
First part of the expanded content for path shell\open\command.<br><br>

```
System.Security.Cryptography.AesCryptoServiceProvider
```
<br>

**Answer: AES**<br><br>

**Q11. What is the child process of our file?**<br><br>

**Answer: powershell.exe**<br><br>


