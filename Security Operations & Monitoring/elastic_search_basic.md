Series from RangeForce <br />
**Problem Description**
You recently started working in the SOC of the Commensurate Technology. There is an issue with a server on the internal network. It has random CPU spikes, and users complain about poor performance.

Elastic Stack has been recently set up. You start to familiarize yourself with the Kibana interface. Maybe you can even find out the root cause of the server performance issues.

**Network Topology**



ELK Interface

Enterprise Search: makes system searchable internally <br />
Observability: monitors your apps for performance, bugs, user experience, etc <br />
Security: system to protect, detect, respond and hunt for security operations <br />
Analytics: general data exploration tools such as searching or creating graphs and dashboards <br />


Discover under Analytics, we can search for queries, enter a time range and apply filter <br />

To view deatils of a particular event, click on the drop down button <br />

Search for authentications to see if there is anything suspicious going on. Each search consist of: <br />
- Index pattern: what elastic search indicies you are working with. Not optional. To create new index; Management > Stack Management > Kibana > Index Patterns
- Time range; since elastichsearch store logs which are time-baassed events, there several options specifying the time
- Filters; filter data by a particular condition. Suitable operations are; is, is not, is one of, is not one of, is between.
- Search Query: search based on the query language. Ex: we are using KQL. So a suitable search query for authentication  is: event.category:"authentication"


**Dashboard**
Helps us with visualization. Gives us aquick overview of what is going on










