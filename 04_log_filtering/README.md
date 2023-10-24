# 04 - Log Filtering

1. Add a custom log to the Log Analytics Workspace
    - add your failed_rdp.log to the Workspace

2. In the Log Analytics, create a custom query to organize your logs using KQL (example below)

Sample KQL Query
```
FAILED_RDP_WITH_GEO_CL
| parse RawData with * "latitude:" latitude ",longitude:" longitude ",destinationhost:" destinationhost ",username:" username ",sourcehost:" sourcehost ",state:" state ", country:" country ",label:" label ",timestamp:" timestamp
| project latitude, longitude, destinationhost, username, sourcehost, state, label, timestamp
```