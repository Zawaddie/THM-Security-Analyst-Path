# Elastic Stack: The Basics

 
Although ELK is not a traditional SIEM, many SOC teams use it like one because of its data searching and visualizing capability. 

**Learnt:**

- how the Elastic Stack (ELK) can be used for log analysis and investigations.
- how the components of ELK and learn how log analysis can be performed through it. 
- how to create visualizations and dashboards in ELK.

---

Elastic Stack (ELK) was originally developed to store, search, and visualize large amounts of data. 

Was used it to monitor application performance and perform searches on large datasets. 

Over time, its features made it popular in security operations as well. Now, many SOC teams use ELK almost as a SIEM solution. 

Elastic Stack is a collection of different open-source components that work together to:
- collect data from any source,
- store and search it, and
- visualize it in real time.

<img width="1333" height="464" alt="image" src="https://github.com/user-attachments/assets/c72dd4b0-2aa5-4081-97d9-b4f4b33e95b0" />

**ELK's core components:**

**Note:** As a SOC analyst, your primary responsibility is to work with ELK to perform log analysis and investigations and no need to necessarily specialize in how each component behind the ELK works. 

1. **Elasticsearch**

 A full-text search and analytics engine for JSON-formatted documents. 
 It stores, analyzes, and correlates data and supports a RESTful API for interacting with it.

2. **Logstash**

A data processing engine that takes data from different sources, filters it, or normalizes it, and then sends it to the destination, which could be Kibana or a listening port.

A Logstash configuration file is divided into three parts, as shown below.

- The Input part is where the user defines the source from which the data is being ingested.
- The Filter part is where the user specifies the filter options to normalize the log ingested above. 
- The Output part is where the user wants the filtered data to be sent. It can be a listening port, Kibana Interface, Elasticsearch database, or file. 

Logstash supports many Input, Output, and Filter plugins.

<img width="339" height="528" alt="image" src="https://github.com/user-attachments/assets/88f73aa6-ea9a-4994-bd87-2c7ce3caabbb" />

3. **Beats**

These are host-based agents known as data-shippers that transfer data from the endpoints to Elasticsearch.
Each beat is a single-purpose agent that sends specific data to Elasticsearch.

Available beats:

<img width="1343" height="606" alt="image" src="https://github.com/user-attachments/assets/565f63a5-6af9-4b80-ac58-964a6c8118d6" />

4. **Kibana**

A web-based data visualization tool that works with Elasticsearch to analyze, investigate, and visualize data streams in real time. 

It allows users to create multiple visualizations and dashboards for better visibility. There is more on Kibana in the following tasks.

How all the components of the Elastic Stack work together step-by-step:

- Beats collect data from multiple agents. For example, Winlogbeat collects Windows event logs, and Packetbeat collects network traffic flows.
- Logstash collects data from beats, ports, or files, parses/normalizes it into field value pairs, and stores them into Elasticsearch.
- Elasticsearch acts as a database used to search and analyze data.
- Kibana is responsible for displaying and visualizing the data stored in Elasticsearch. The data stored in Elasticsearch can easily be shaped into different visualizations, time charts, infographics, etc., using Kibana.

<img width="1143" height="363" alt="image" src="https://github.com/user-attachments/assets/e793ecab-c09c-48cf-b666-c911539cd37d" />

---

## **HANDS-ON WITH ELK**

<img width="1364" height="503" alt="image" src="https://github.com/user-attachments/assets/99d22644-a20e-4e31-b907-99c3c5a3185b" />

<img width="1364" height="484" alt="image" src="https://github.com/user-attachments/assets/0f6d9746-beb9-4a33-98cc-debc9aa00e31" />

ELK's front-end interface are the main features that a SOC analyst operates on.

Kibana is the component of ELK that supports these interactions with the front end.

1. **DISCOVER TAB**

<img width="1365" height="491" alt="image" src="https://github.com/user-attachments/assets/47ce0368-b4e2-4529-b72f-018cf4e07a59" />

<img width="1365" height="487" alt="image" src="https://github.com/user-attachments/assets/8dbc1120-51e6-4fe1-a147-189e5370e6c2" />


The Discover tab is where the SOC analysts spend most of their time. 

This tab shows the ingested logs, the search bar, normalized fields, and more. 

Analysts can search for the logs, investigate anomalies, and apply filters based on search terms and time periods.

<img width="1352" height="604" alt="image" src="https://github.com/user-attachments/assets/2eadd754-f3b2-4e81-9164-42b440787c13" />

Note what each element of the Discover tab does: 

1. **Logs**

Each row shows a single log containing information about the event, along with the fields and values found in that log.

2. **Fields Pane**
   
The left panel of the interface shows the list of fields parsed from the logs. 
We can click on any field to add it to the filter or remove it from the search.

3. **Index Pattern**

Each type of log is stored in a different index pattern. We can select the index pattern from which we need the logs. For example, for VPN logs, we would need to select the index pattern in which VPN logs are stored.

4. **Search Bar**

It is a place where the user adds search queries and applies filters to narrow down the results. In the next task, we will learn how to perform searches through queries.

5. **Time Filter**

We can narrow down results based on any specific time duration. 

6. **Time Interval**

This chart shows the event counts over time.

7. **TOP Bar**

This bar contains various options to save the search, open the saved searches, share or save the search, etc.

8. **Discover Tab**

This is the main workspace in Kibana for exploring, searching, and analyzing raw data.

9. **Add Filter**
We can apply filters to specific fields to narrow down results, rather than manually typing entire queries.

---

**Index Pattern**

By default, Kibana requires an index pattern to access the data stored/ingested in Elasticsearch. 

It tells Kibana which elasticsearch data we want to explore. Each Index pattern corresponds to certain defined properties of the fields. A single index pattern can point to multiple indices.

Each log source has a different log structure; therefore, when logs are ingested into Elasticsearch, they are first normalized into corresponding fields and values by creating a dedicated index pattern for the data source.

<img width="510" height="373" alt="image" src="https://github.com/user-attachments/assets/2e4c45b4-6afb-490d-8e0a-7296c4cff04b" />

**Fields Pane**

The left panel in the Discover tab shows the list of the normalized fields it finds in the available logs. Clicking on any field, shows the top 5 values and the percentage of occurrence.

We can use these values to apply filters to them. Clicking on the + button will add a filter to show the logs containing this value, and the - button will add a filter to show the results that do not have this value.

<img width="725" height="503" alt="image" src="https://github.com/user-attachments/assets/eb720e2d-4448-4e18-8298-96b5eb190580" />

We can also apply filters to any of the fields shown in the panel on the left. 

All we have to do is click the *Add filter* option under the search bar, which will allow us to apply a filter to the fields.

<img width="1290" height="609" alt="image" src="https://github.com/user-attachments/assets/b1c69e8a-f77b-40ec-8681-44077f8f4c60" />

**Timeline***

The timeline pane provides an overview of the number of events that occurred for the specific time/date. 

We can only select the bar to show the logs in that period. The count at the top left displays the number of events found in the specified time.

<img width="1356" height="217" alt="image" src="https://github.com/user-attachments/assets/2d5aadc2-e7ac-4857-aff6-4a7ae83c06d2" />


This bar is also helpful in identifying the spike in the logs. for instance, we can note an unusual log spike on 11th January 2022.

**Create Table**

By default, the logs are shown in raw form. We can click on any log and select important fields to create a table showing only those fields. 

This method reduces the noise and makes it more presentable and meaningful.

You can also save the table format once it is created. It will then show the same fields every time a user logs into the dashboard.

## PRACTICAL

Q1. Select the index vpn_connections and filter from 31st December 2021 to 2nd Feb 2022. 2861 hits are returned.

<img width="1362" height="490" alt="image" src="https://github.com/user-attachments/assets/4042a1df-99f5-4808-ae1c-1bb9163b4835" />


Q2. 238.163.231.224, is the  IP address that has the maximum number of connections?

<img width="1364" height="488" alt="image" src="https://github.com/user-attachments/assets/7fbb1a0f-9fe2-4d49-9752-cdc92a0a28e6" />


Q3. User "James" is responsible for the overall maximum traffic

<img width="1364" height="493" alt="image" src="https://github.com/user-attachments/assets/c64a6272-f98f-49a0-b57c-425a8100f270" />


Q4. After apply Filter on UserName Emanda; 107.14.1.247 is the SourceIP has max hits.

<img width="1356" height="494" alt="image" src="https://github.com/user-attachments/assets/10759337-d7dd-4ea9-8d1c-86a838a32118" />


Q5. On 11th Jan, the IP, 172.201.60.191 caused the spike observed in the time chart.

<img width="1356" height="497" alt="image" src="https://github.com/user-attachments/assets/48a6f60d-dc66-421f-ac4b-de461463a498" />


Q6. 48 connections were observed from IP 238.163.231.224, excluding the New York state.

<img width="1365" height="497" alt="image" src="https://github.com/user-attachments/assets/62b36545-569a-4424-b97f-36b9b1fc736f" />


Q7. Create a table with the fields IP, UserName, Source_Country and save.

---

## KQL OVERVIEW

With the 'Search Bar' in the 'Discover Tab, we can find anything.

KQL (Kibana Query Language) is a search query language used to search the ingested logs/documents in Elasticsearch inside this search bar to perform our searches.

<img width="1130" height="379" alt="image" src="https://github.com/user-attachments/assets/c6b41b7b-f093-4823-a5d7-51798fcee499" />

With KQL, we can search for the logs in two different ways.

- Free text search
- Field-based search

1. **Free text Search**

This allows users to search for logs based on text only. 

That means a simple search of the term security will return all the documents that contain this term, irrespective of the field. 
The search for the text *'United States'* in the search bar returns all the logs that contain this term, regardless of the place or the field. 

<img width="1348" height="523" alt="image" src="https://github.com/user-attachments/assets/9f9fe718-da55-4569-b635-422347bb2a7e" />

Serching for the term *'united'* doesn't return any results because KQL looks for the whole term/word in the documents.

<img width="1352" height="514" alt="image" src="https://github.com/user-attachments/assets/ab7fb929-0b29-4d61-a0ac-a4b566b3b0e8" />

KQL allows the wildcard * to match parts of the word. Let's find out how to use this wild card in the search query. Using the wildcard with the term 'United' returns all the results containing the term United and any other term after it.

<img width="1356" height="527" alt="image" src="https://github.com/user-attachments/assets/ad09fd67-e5fa-42c0-8665-cf68c99af9a6" />

**LOGICAL OPERATORS (AND | OR | NOT)**

KQL also allows users to utilize logical operators in the search query:

1. **AND Operator**

we use the AND Operator to create a search that returns the logs containing the terms "United States" and "Virginia".

Search Query: *"United States" AND "Virginia"*


<img width="1363" height="490" alt="image" src="https://github.com/user-attachments/assets/330333ea-a88d-41c6-8dfe-15df7b0d04b6" />

Shows results for United States AND Virginia

2. **OR Operator**

We will use the OR operator to show logs that contain either the United States or England.

Search Query: *"United States" OR "England"*

<img width="1365" height="490" alt="image" src="https://github.com/user-attachments/assets/bbbef9b2-bc98-457c-87fd-1463f2b26794" />

Shows results for the term United States OR England

3. **NOT Operator**

The NOT Operator cab be used to remove a particular term from the search results. This search query will show the logs from the United States, including all states, but ignoring Florida.

Search Query: *"United States" AND NOT ("Florida")*

<img width="1361" height="506" alt="image" src="https://github.com/user-attachments/assets/c6778fa0-e047-4238-84fe-52e4f354425d" />

Shows result for United States AND NOT Florida


2. **Field-based search**


In the Field-based search, we provide the field name and the value we are looking for in the logs. 

This search has a special syntax as *Field: Value*. It uses a colon as a separator between the field and the value. 

Search Query: *Source_ip : 238.163.231.224 AND UserName : Suleman*

<img width="1358" height="502" alt="image" src="https://github.com/user-attachments/assets/9fb78dbb-9dae-4230-8c56-aa00ba352a99" />
Shows result for Source_ip : 238.163.231.224    AND     UserName : Suleman

When we click on the search bar, we are presented with all the available fields that we can use in our search query. 

<img width="1364" height="506" alt="image" src="https://github.com/user-attachments/assets/f5e13ea2-4001-4cb1-9642-b2de1442f46d" />

**QUiz**

Q1. Create a search query to filter the logs where Source_Country is the United States and show logs from User James or Albert. How many records were returned?

Search Query: *Source_Country : "United States"  AND UserName : "James"  OR UserName : "Albert"*

<img width="1364" height="480" alt="image" src="https://github.com/user-attachments/assets/6e35c202-da35-4658-8459-9e7779191341" />


Q2. A user Johny Brown was terminated on the 1st of January, 2022. Create a search query to determine how many times a VPN connection was observed after his termination.

<img width="1351" height="488" alt="image" src="https://github.com/user-attachments/assets/835ed0f1-dbb0-4983-bf8a-033c5a245d48" />

---

## Creating Visualizations

The visualization tab allows us to visualize the data in different forms such as tables, pie charts, bar charts, etc. 

There are a few ways to navigate to the visualization tab. One way is to click on any field in the discover tab and click on the visualization.

We can create multiple visualizations by selecting options like tables, pie charts, etc.

Correlation Option
Often, we require creating correlations between multiple fields. Dragging the required field in the middle will create a correlation tab in the visualization tab. Here, we selected the Source_Country as the second field to show a correlation among the client Source_IP.

We can also create a table to show the values of the selected fields as columns

The most important step in creating these visualizations is saving them. To do so, click on the save Option on the right side and fill in the descriptive values below. 

Steps to take after creating Visualizations:

Create a visualization and click the Save button at the top right corner.
- Add the title and description to the visualization.
- Click Save and add to the library when it's done.

**Failed Connection Attempts Visualization**

We create a table to show the user and the IP address involved in failed attempts.

<img width="1361" height="490" alt="image" src="https://github.com/user-attachments/assets/c65f53f0-f36f-4aa6-abe6-de0aeb5fd55f" />

<img width="1364" height="486" alt="image" src="https://github.com/user-attachments/assets/02d44c1f-5d22-4808-9c72-9b1e8a0faad6" />

Simon has 274 failed login attempts.

---

## Creating Custorm Dashboards

Dashboards provide good visibility into log collection. A user can create multiple dashboards to fulfill a specific need. In this task, we can combine different saved searches and visualizations to create a custom dashboard for VPN log visibility.


After we have saved a few Searches from the Discover tab, created some Visualizations, and saved them, we can explore the dashboard tab and create a custom dashboard. 

The steps to create a dashboard are:

- Go to the Dashboard tab and click on the Create dashboard.
- Click on Add from Library.
- Click on the visualizations and saved searches. It will be added to the dashboard.
- Once the items are added, adjust them accordingly.
- Don't forget to save the dashboard after completing it.










