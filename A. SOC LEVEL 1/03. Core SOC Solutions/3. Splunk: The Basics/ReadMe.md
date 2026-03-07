# Splunk: The Basics

Splunk is one of the leading SIEM solutions in the market. 
It allows users to collect, analyze, and correlate network and machine logs in real time. 

In the room, I was able to explore the basics of Splunk and its functionalities, and how it provides better visibility of network activities that helps speed up detection.

---

**Splunk Components**

<img width="670" height="274" alt="image" src="https://github.com/user-attachments/assets/e2dfd4dd-3baa-4387-a6cd-34af0dfa397b" />


1. **Splunk Forwarder**
   
Splunk Forwarder is a lightweight agent installed on the endpoint intended to be monitored, and its main task is to collect the data and send it to the Splunk instance. 
It does not affect the endpoint's performance as it takes a few resources to process. 

Some of the key data sources are:

- Web server generating web traffic.
- Windows machine generating Windows Event Logs, PowerShell, and Sysmon data.
- Linux host generating host-centric logs.
- Database generating DB connection requests, responses, and errors.

2. **Splunk Indexer**

The forwarder collects the data from the log sources and sends it to the Splunk Indexer.

Splunk Indexer plays the main role in processing the data it receives from forwarders. 
It parses and normalizes the data into field-value pairs, categorizes it, and stores the results as events, making the processed data easy to search and analyze.

Normalized data stored by the indexer, can be searched by the Search Head.

3. **Search Head**

Splunk Search Head is the place within the Search & Reporting App where users can search the indexed logs. 
The searches are done using the SPL (Search Processing Language), a powerful query language for searching indexed data. 
When the user performs a search, the request is sent to the indexer, and the relevant events are returned as field-value pairs.

The Search Head also allows you to transform results into presentable tables and visualizations such as pie, bar, and column charts, as shown below:

---

**Splunk's Homepage***

<img width="1356" height="505" alt="image" src="https://github.com/user-attachments/assets/cbc68930-7566-4709-90a8-cde8c1432b59" />

Splunk can ingest any data. 

According to the [Splunk documentation](https://docs.splunk.com/Documentation/Splunk/8.1.2/SearchTutorial/NavigatingSplunk), when data is added to Splunk, the data is processed and transformed into a series of individual events. 

The data sources can be event logs, website logs, firewall logs, etc and they are grouped into categories.


 A listing from the [Splunk documentation](https://docs.splunk.com/Documentation/Splunk/8.1.2/SearchTutorial/AboutgettingdataintoSplunk) detailing each data source category.

 <img width="695" height="455" alt="image" src="https://github.com/user-attachments/assets/2dbda789-cb72-4df1-8809-d60f4ec4ac72" />

---

**PRACTICAL:**

**Provided:** VPN Logs

Steps to upload the data successfully:

1. **Select Source**: Choose the Log file and the data source.
2. **Select Source Type**: Select what type of logs are being ingested, e.g, JSON, syslog.
3. **Input Settings:** Select the index where these logs will be dumped and the HOSTNAME to be associated with the logs.
4. **Review:** Review all the configurations.
5. **Done:** Complete the upload. Your data will be uploaded successfully and ready to be analyzed.

**File Uploaded Successfully**. It has 2862 events.

<img width="1357" height="471" alt="image" src="https://github.com/user-attachments/assets/11d13d2c-3fac-4aee-bd87-25e431a6f9f2" />


60 Log events are associated with the user "Maleena".

<img width="1361" height="492" alt="image" src="https://github.com/user-attachments/assets/58147fb3-df71-428b-ae38-88a927eee27e" />

**"Smith'** is the user associated with the IP address, 107.14.182.38


<img width="1361" height="495" alt="image" src="https://github.com/user-attachments/assets/bae83c8f-8526-421e-91aa-1285d00aa584" />


2814 events originated from all other courntries and not France:

  <img width="1359" height="491" alt="image" src="https://github.com/user-attachments/assets/645671a4-a4f7-4719-9d9f-63914a3cc1ed" />

48 events are from france

<img width="1361" height="484" alt="image" src="https://github.com/user-attachments/assets/9948b9af-0bef-4fd6-8890-adff743a58d3" />


14 events are associated with the IP address. 107.3.206.58

  <img width="1358" height="489" alt="image" src="https://github.com/user-attachments/assets/bd96af7f-9c30-477f-afde-846d4583fc8d" />

 Other Recommended Splunk walkthrough and challenge rooms to help understand how Splunk is effectively used in investigating incidents.

- [Splunk: Exploring SPL](https://tryhackme.com/room/splunkexploringspl)
- [Incident Handling with Splunk](https://tryhackme.com/room/splunk201)
- [Investigating With Splunk](http://tryhackme.com/jr/investigatingwithsplunk)
- [Benign - Challenge](http://tryhackme.com/jr/benign)
- [PoshEclipse - Challenge](http://tryhackme.com/jr/posheclipse)





