# 03 - Virtual Machine modifications

1. Connect to the virtual machine via RDP using the public IP address

2. Turn off all firewall settings on the VM

3. Get a free API key from ipgeolocation.io

4. Download the Powershell script from ```https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1```

5. Add your API key to the Powershell script
---Sample from Josh Madakor's powershell script---
```shell
﻿# Get API key from here: https://ipgeolocation.io/
$API_KEY      = "ENTER_API_KEY_HERE"
$LOGFILE_NAME = "failed_rdp.log"
$LOGFILE_PATH = "C:\ProgramData\$($LOGFILE_NAME)"

# This filter will be used to filter failed RDP events from Windows Event Viewer
$XMLFilter = @'
<QueryList> 
   <Query Id="0" Path="Security">
```
This script does the following:
- Pulls failed logon events from event viewer
- Uses the API key to find geolocation information based of the IP of the attacker
- Outputs the logs into a text file in C:\ProgramData\failed_rdp.log for the Azure Log Analytics Engine to pull

# Sample output from Log file

```
latitude:50.43830,longitude:30.45675,destinationhost:honeypot-vm1,username:estimating,sourcehost:185.156.72.22,state:Kyiv City, country:Ukraine,label:Ukraine - 185.156.72.22,timestamp:2023-10-19 08:53:12
latitude:47.01479,longitude:28.85662,destinationhost:honeypot-vm1,username:administrator,sourcehost:212.56.195.102,state:Kishinev, country:Moldova,label:Moldova - 212.56.195.102,timestamp:2023-10-19 08:53:11
latitude:50.43830,longitude:30.45675,destinationhost:honeypot-vm1,username:data,sourcehost:185.156.72.22,state:Kyiv City, country:Ukraine,label:Ukraine - 185.156.72.22,timestamp:2023-10-19 08:53:10
latitude:47.01479,longitude:28.85662,destinationhost:honeypot-vm1,username:administrator,sourcehost:212.56.195.102,state:Kishinev, country:Moldova,label:Moldova - 212.56.195.102,timestamp:2023-10-19 08:53:09
latitude:47.01479,longitude:28.85662,destinationhost:honeypot-vm1,username:administrator,sourcehost:212.56.195.102,state:Kishinev, country:Moldova,label:Moldova - 212.56.195.102,timestamp:2023-10-19 08:53:08
latitude:55.79762,longitude:37.60087,destinationhost:honeypot-vm1,username:karleen,sourcehost:109.107.183.74,state:Central Federal District, country:Russia,label:Russia - 109.107.183.74,timestamp:2023-10-19 08:53:07
latitude:47.01479,longitude:28.85662,destinationhost:honeypot-vm1,username:administrator,sourcehost:212.56.195.102,state:Kishinev, country:Moldova,label:Moldova - 212.56.195.102,timestamp:2023-10-19 08:53:06
```