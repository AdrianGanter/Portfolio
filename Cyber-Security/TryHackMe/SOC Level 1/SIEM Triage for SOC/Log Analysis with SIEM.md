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


