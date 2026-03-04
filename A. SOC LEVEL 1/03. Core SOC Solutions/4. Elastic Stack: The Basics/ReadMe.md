# Elastic Stack: The Basics

 
Although ELK is not a traditional SIEM, many SOC teams use it like one because of its data searching and visualizing capability. 

**Learnt:**

- how the Elastic Stack (ELK) can be used for log analysis and investigations.
- how the components of ELK and learn how log analysis can be performed through it. 
- how to create visualizations and dashboards in ELK.

---

Elastic Stack (ELK) was originally developed to store, search, and visualize large amounts of data. 

Organizations used it to monitor application performance and perform searches on large datasets. 

Over time, its features made it popular in security operations as well. Now, many SOC teams use ELK almost as a SIEM solution. 

Elastic Stack is a collection of different open-source components that work together to:
- collect data from any source,
- store and search it, and
- visualize it in real time.

<img width="1333" height="464" alt="image" src="https://github.com/user-attachments/assets/c72dd4b0-2aa5-4081-97d9-b4f4b33e95b0" />

Before we go on to learning log analysis through ELK, let's first discuss its core components.

Note: As a SOC analyst, your primary responsibility is to work with ELK to perform log analysis and investigations. You do not need to specialize in how each component behind the ELK works. However, taking a basic understanding of these components is essential. 

1. Elasticsearch
2. 
The first component, Elasticsearch, is a full-text search and analytics engine for JSON-formatted documents. It stores, analyzes, and correlates data and supports a RESTful API for interacting with it.

3. Logstash
Logstash is a data processing engine that takes data from different sources, filters it, or normalizes it, and then sends it to the destination, which could be Kibana or a listening port. A Logstash configuration file is divided into three parts, as shown below.

The Input part is where the user defines the source from which the data is being ingested.
The Filter part is where the user specifies the filter options to normalize the log ingested above. 
The Output part is where the user wants the filtered data to be sent. It can be a listening port, Kibana Interface, Elasticsearch database, or file. 
Logstash supports many Input, Output, and Filter plugins.

<img width="339" height="528" alt="image" src="https://github.com/user-attachments/assets/88f73aa6-ea9a-4994-bd87-2c7ce3caabbb" />

3. Beats
Beats are host-based agents known as data-shippers that ship/transfer data from the endpoints to Elasticsearch.
Each beat is a single-purpose agent that sends specific data to Elasticsearch.

All available beats are shown below.






