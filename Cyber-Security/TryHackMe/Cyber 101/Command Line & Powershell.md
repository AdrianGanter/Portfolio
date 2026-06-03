### Windows CLI & PowerShell

#### Windows Command Prompt (cmd.exe)
| Task | Command |
|---|---|
| OS / system info | `ver` ‑> `systeminfo` |
| Network reachability | `ping 8.8.8.8` |
| Route trace | `tracert target.com` |
| DNS lookup | `nslookup target.com` |
| Active connections | `netstat -ano` |
| List directory (hidden incl.) | `dir /a` |
| Recursive file search | `dir /s *.exe` |
| Wildcard copy | `copy *.log C:\Logs\` |
| Kill process | `taskkill /PID <PID>` |
| Live services | `tasklist` |
| Disk & integrity checks | `chkdsk C:` / `sfc /scannow` |

#### Windows PowerShell (PS)
| Task | Cmdlet |
|---|---|
| Help with examples | `Get-Help <cmdlet> -examples` |
| Discover cmdlets | `Get-Command *service*` |
| List items | `Get-ChildItem -Path C:\Tools` |
| Change dir | `Set-Location C:\` |
| Read file | `Get-Content file.txt` |
| Create / Remove | `New-Item -ItemType File` / `Remove-Item` |
| Copy / Move | `Copy-Item src dst` / `Move-Item src dst` |
| System inventory | `Get-ComputerInfo` |
| IP config | `Get-NetIPConfiguration` |
| Active TCP | `Get-NetTCPConnection` |
| Running processes | `Get-Process` |
| File integrity | `Get-FileHash file.exe -Algorithm SHA256` |
| Filter objects | `Get-ChildItem \| Where-Object {$_.Extension -eq ".txt"}` |

> Remember: append `| more` to paginate long outputs, or use `/?` (`Get-Help`) for built-in help on any command.
