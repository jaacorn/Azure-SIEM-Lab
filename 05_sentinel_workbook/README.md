# 05 - Setting up Azure Sentinel Workbook

1. In Sentinel, create a new workbook

2. Clear existing queries, and add a new query with your custom KQL query
```
FAILED_RDP_WITH_GEO_CL
| parse RawData with * "latitude:" latitude ",longitude:" longitude ",destinationhost:" destinationhost ",username:" username ",sourcehost:" sourcehost ",state:" state ", country:" country ",label:" label ",timestamp:" timestamp
| where sourcehost != ""
| summarize event_count=count() by username, state, country, latitude, longitude, destinationhost, sourcehost, label, timestamp
```
This is the final query I ended with to view the results on a map

3. Set your query to be displayed by world map

Note: I also created a second query to display top 10 most common user names attempted. All done via KQl queries. Picure of the map is in the pictures directory.