#  LOLBins (Living Off the Land Binaries)

##  What Are LOLBins?
- Legitimate, built-in system tools  
- Signed and trusted by Microsoft  
- Abused by attackers for malicious actions  
- No malware dropped on disk  

---

## Why It Matters
- Fileless attacks → harder to detect  
- Blends with admin activity  
- Bypasses traditional AV/EDR  
- Widely used in modern attacks  

---

##  Common LOLBins

### PowerShell
- In-memory execution  
- Payload download  
- Persistence  

###  WMIC
- Remote execution  
- Reconnaissance  
- Lateral movement  

###  PsExec
- Remote command execution  
- Ransomware spread  
- Privilege escalation  

---

##  Detection & Defense

###  Logging
- PowerShell logs (4103, 4104)  
- Process creation (4688)  
- WMI logs  

###  Behavior Monitoring
- Office → PowerShell spawning  
- Encoded commands (`-enc`)  
- Non-admin use of admin tools  

### Controls
- AppLocker / WDAC  
- Least privilege  
- Restrict remote execution  

### Network Monitoring
- Outbound connections  
- SMB lateral movement  
- Remote service creation  

### Threat Hunting
- Encoded scripts  
- Suspicious WMI usage  
- Multi-host execution  

---

