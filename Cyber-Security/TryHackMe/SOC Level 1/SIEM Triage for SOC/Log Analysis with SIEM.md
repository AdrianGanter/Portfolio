Windows Logs Scenario
You are an SOC Level 1 Analyst on shift and have received an alert indicating a suspicious network connection using port 5678 on the WIN-105 host. Your task is to conduct an investigation and determine whether this activity is suspicious.

I began searching for Network events with Event Code 3, and specified the host machine and destination port. I also made sure to include Image in the table, to see what process created the connection.
| table _time EventCode ComputerName Image SourceIp SourcePort DestinationIp DestinationPort Protocol`

<img width="1361" height="483" alt="image" src="https://github.com/user-attachments/assets/a5001ffb-bdec-4887-9a6f-5604eb3a7963" />

It appears a process C:\Windows\Temp\SharePoInt.exe had initiated the suspicious connection

To find malicious hash value or the potentially malicious process I searched: `index=task4 EventCode=1 Image="C:\\Windows\\Temp\\SharePoInt.exe"`
<img width="1360" height="614" alt="image" src="https://github.com/user-attachments/assets/5da56a64-a104-4f33-91a7-5167c18921dc" />

Exploring the details of the event, I found the hash value: 770D14FFA142F09730B415506249E7D1

I then proceeded to search for any scheduled tasks this process may have created with a simple search of
`index=task4 schtasks SharePoInt.exe`
I recieved 4 related hits, and one of them shows the scheduled task Office365 Install was created.
<img width="1363" height="617" alt="image" src="https://github.com/user-attachments/assets/56c4ed0e-b76d-4e87-b0ab-92a840731256" />

---

Linux Logs Scenario

You are a SOC Level 1 Analyst on shift and have received an alert indicating possible persistence through the creation of a new remote-ssh user on an Ubuntu server. Your task is to dive into the logs and determine exactly what happened on the system.

Firstly I started off with searching for the remote-ssh user with the query
`index=task5 source="auth.log"
| search "remote-ssh"`

<img width="1189" height="395" alt="image" src="https://github.com/user-attachments/assets/828493f0-c772-4b1f-b2df-5107a061a068" />

I identify the creation time and date of the user among historical events of user group creation and the original root user who created the new user remote-ssh identified as "jack-brown"

<img width="1084" height="102" alt="image" src="https://github.com/user-attachments/assets/e28e4b8f-1a93-4904-9201-78a0301e033e" />

Refining the search with the discovered user jack-brown, I learned the user was logged in successfully from IP address 10.14.94.82
`index=task5 source="auth.log" user="jack-brown" 
| search "Accepted Password"`
<img width="1108" height="201" alt="image" src="https://github.com/user-attachments/assets/4aea101b-131a-4f14-9af5-e67cf82ab0ce" />

So interestingly I looked into how many failed login attempts occurred to detect any means of brute force. With the query
`index=task5 source="auth.log" user="jack-brown" 
| search "Failed Password"`
it was discovered that 4 failed attempts occurred within 33 seconds on a persistent port of 54446


<img width="1143" height="399" alt="image" src="https://github.com/user-attachments/assets/e884f4cd-b1c7-48e8-9fd9-19f07af6bf3c" />

To identify the port the persistence mechanism is configured to connect to, i searched 
`index=task5 source=syslog ("CRON" OR "cron")`
This revealed 2 events. One of major concern indicates a python reverse shell connection on IP 10.10.33.31 on port number 7654

<img width="1112" height="300" alt="image" src="https://github.com/user-attachments/assets/e59645fc-8880-4462-a3e8-b5e1f77dd77b" />

---

Web Logs Scenario

You are a SOC Level 1 Analyst on shift and have received an alert indicating a spike in activity on the organisation's web server.
Your task is to dive into the logs and determine exactly what happened.

I started looking into which URI path had the highest amount of requests with this query:
`index=task6
| search uri_path IN(*.php, *.phtm, *.asp, *.aspx, *.jsp, *.exe)
| stats values(status) as status values(useragent) as UserAgent values(method) as method values(clientip) as clientip count by uri
| where count > 2 
| table referer_domain count method status clientip UserAgent uri`

it was revealed that wp-login.php had the largest request amount of 905
<img width="1238" height="440" alt="image" src="https://github.com/user-attachments/assets/22d6edfa-5e92-46f9-bec1-8cf1d2fdd205" />

Changing the query slightly I was able to identify the culprit IP address for most of the requests. A total of 603 came from the IP address: 10.10.243.134 

<img width="985" height="447" alt="image" src="https://github.com/user-attachments/assets/87062ff0-de9c-4e81-b17c-80e42af514d3" />

Looking at the data, the IP address has used a tool called wpscan. This tool and request volume supports behavior that closely aligns to brute force.
