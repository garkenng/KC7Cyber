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



