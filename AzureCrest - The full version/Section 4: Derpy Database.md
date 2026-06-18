## AzureCrest - The full version: Section 4: Derpy Database<br>

**Q1. This Twitter user, also known as "Hutch", co-authored the paper that introduced the Cyber Kill Chain to information security. (enter their @ username)**<br><br>

**Answer: @killchain**<br><br>

**Q2. What is the first step of the Cyber Kill Chain?**<br><br>


**Answer: Reconnaissance**<br><br>

**Q3. How many records are there of the threat actor browsing the Azure Crest Hospital's website?**<br><br>
First is to look for url with the keyword search in, to see what searches have been carried out on the hospital website.<br><br>

```
InboundNetworkEvents
| where url contains "search"
```
<br>

Looking at the different user agents, one agent is of interest.<br><br>

```
Opera/9.63.(Windows CE; lb-LU) Presto/2.9.161 Version/12.00
```
<br>

Run search for inbound traffic with that user agent.<br><br>

```
InboundNetworkEvents
| where user_agent == "Opera/9.63.(Windows CE; lb-LU) Presto/2.9.161 Version/12.00"
```
<br>

Looking through the url column, the threat actor is searching for information which not deemed normal.<br><br>

```
How many money does Azure Crest Hospital have
Azure Crest Hospital financial statements
```
<br>

**Answer: 32**<br><br>


**Q4. What article did they read about personnel changes at the hospital? (provide full url)**<br><br>
Looking through links visited on hospital website.<br><br>

**Answer: https://azurecresthospital.med/news/half-of-it-department-fired**<br><br>

**Q5. Which employee was hired as part of an effort to reduce costs?**<br><br>
Looking through links visited on hospital website.<br><br>

```
https://azurecresthospital.med/news/roy-trenemman-joins-azure-crest-to-save-money-on-erp-systems
```
<br>

**Answer: Roy Trenneman**<br><br>


**Q6. What article did Azure Crest publish about building one's own stuff instead of paying for it? (provide the full url)**<br><br>


**Answer: https://azurecresthospital.med/news/research/why-running-your-own-erp-systems-is-a-good-idea**<br><br>

**Q7. What specific type of medical records was the Threat Actor attempting to access on Azure Crest Hospital’s internal share?**<br><br>

```
InboundNetworkEvents
| where url contains "medical"
```
<br>

```
https://azurecresthospital.med/search=pediatric+patient+medical+history
https://azurecresthospital.med/internal_share/medical_records/pediatric
```
<br>

**Answer: pediatric**<br><br>

**Q8. Which employee did the threat actor ultimately decide to target?**<br><br>

```
https://azurecresthospital.med/search=Roy+Trenemman+Azure+Crest
```
<br>

**Answer: Roy Trenneman**<br><br>

**Q9. What is that employee's role?**<br><br>

```
Employees
| where name == "Roy Trenneman"
```
<br>

**Answer: Database Administrator**<br><br>

**Q10. What is the timestamp of the email that the threat actor sent to that employee?**<br><br>

```
Email
| where recipient == "roy_trenneman@azurecresthospital.med"
| where sender == "medstaffinfo@hospitalcomm.org" or sender == "healthupdate@gmail.com"
```
<br>

**Answer: 3/4/2024, 10:52:18 AM**<br><br>

**Q11. Did that employee click on the link? (yes/no)**<br><br>

```
OutboundNetworkEvents
| where src_ip == "10.10.0.2"
| where url == "http://unhealthyrecordsystems.tech/images/images/New_Healthcare_Protocols.docm"
```
<br>
One result is returned, so the link was clicked.<br><br>

**Answer: yes**<br><br>

**Q12. What is the timestamp for when the docm file was created on Roy's machine?**<br><br>

```
FileCreationEvents
| where hostname == "SUPER-DB-SERVER-9000"
| where filename contains ".docm"
```
<br>

**Answer: 3/4/2024, 11:28:57 AM**<br><br>

**Q13. What is the name of the first malicious file created by the threat actor in the user's Temp folder?**<br><br>

```
FileCreationEvents
| where hostname == "SUPER-DB-SERVER-9000"
| where path contains "temp"
| where timestamp > datetime(3/4/2024, 11:28:57 AM)
```
<br>

**Answer: dbhunter.exe**<br><br>


**Q14. What types of files does dbhunter.exe search for upon execution? (enter any one of them)**<br><br>

```
ProcessEvents
| where process_name == "dbhunter.exe"
```
<br>

```
dbhunter.exe --search --filetype .db .sql .mdb --output C:\\In\\found_databases.txt
```
<br>

**Answer: .db**<br><br>

**Q15. What password is used to encrypt the compressed file containing Roy's meme collection?**<br><br>

```
ProcessEvents
| where process_commandline contains ".mdb"
```
<br>

```
7z.exe a -t7z C:\\Out\\Roys_Meme_Collection.7z C:\\Out\\*meme*.mdb -p mommawemadeit
```
<br>

**Answer: mommawemadeit**<br><br>

**Q16. What extension has been added to the files to indicate that they have been encrypted?**<br><br>
Using the timestamp from the previous question, see what extension name is when files were encrypted.<br><br>

```
FileCreationEvents
| where timestamp > datetime(4/2/2024, 11:31:47 AM)
```
<br>

Taking the first result.<br><br>

```
C:\Users\rotrenneman\Downloads\billion.odt.scholopendra
```
<br>

**Answer: .scholopendra**<br><br>

**Q17. What is the name of the new wallpaper?**<br><br>

```
FileCreationEvents
| where hostname == "SUPER-DB-SERVER-9000"
| where filename contains ".jpg"
```
<br>

```
C:\In\ItWentWrong.jpg
```
<br>

**Answer: ItWentWrong.jpg**<br><br>
