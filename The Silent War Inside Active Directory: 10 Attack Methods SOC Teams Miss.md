#  The Silent War Inside Active Directory

Active Directory (AD) is the core identity system in most enterprise environments — and one of the most targeted attack surfaces in cybersecurity.

This repository summarizes **10 critical Active Directory attack techniques**, how they work, how to detect them, and how to mitigate them, mapped to MITRE ATT&CK.

---

##  Overview

AD compromise often leads to full domain takeover. Attackers rarely exploit "zero-days" — instead, they abuse:

- Misconfigurations
- Legacy protocols
- Weak service accounts
- Excessive privileges
- Poor visibility in logging

---

##  Top 10 Active Directory Attack Techniques

### 1. Kerberoasting (T1558.003)
Attackers request service tickets (TGS) and crack them offline to retrieve service account passwords.

**Detection:** Event ID 4769 (RC4 encryption spikes)

---

### 2. Password Spraying (T1110.003)
Single password tried across many accounts to avoid lockouts.

**Detection:** Event ID 4625 across multiple users from same IP

---

### 3. LLMNR/NBT-NS Poisoning (T1557.001)
Broadcast name resolution spoofing to capture NTLM hashes.

**Detection:** Suspicious LLMNR traffic (UDP 5355)

---

### 4. Pass-the-Hash (T1550.002)
Use NTLM hashes from LSASS to authenticate without passwords.

**Detection:** Sysmon Event ID 10 (LSASS access anomalies)

---

### 5. ACL Privilege Escalation (T1484.001)
Misconfigured permissions (GenericAll, WriteDACL) enable stealth escalation paths.

**Detection:** BloodHound path analysis

---

### 6. LDAP Reconnaissance (T1018 / T1087)
Enumerating AD structure using legitimate queries.

**Detection:** Event ID 1644 (high-volume LDAP queries)

---

### 7. BloodHound Recon (T1069 / T1482)
Graph-based attack path discovery from low-privilege to Domain Admin.

**Detection:** SharpHound query patterns in LDAP logs

---

### 8. NTDS.dit Extraction / DCSync (T1003.003)
Replication abuse or file extraction to obtain all domain password hashes.

**Detection:** Event ID 4662 (replication access)

---

### 9. Default / Hardcoded Credentials (T1078.002)
Weak or reused service credentials stored in scripts or GPOs.

**Detection:** SYSVOL inspection + credential reuse patterns

---

### 10. Golden / Silver Ticket Attacks (T1558.001)
Forged Kerberos tickets using krbtgt or service account hashes.

**Detection:** Impossible logon patterns, krbtgt anomaly signals

---

## Detection Strategy

- Event ID 4625 → Password spraying
- Event ID 4769 → Kerberoasting
- Event ID 4662 → DCSync / replication abuse
- Event ID 1644 → LDAP enumeration

---

##  Hardening Recommendations

✔ Disable LLMNR & NBT-NS  
✔ Enforce AES Kerberos encryption (disable RC4)  
✔ Deploy Credential Guard  
✔ Implement tiered administration (PAW model)  
✔ Replace service accounts with gMSA  
✔ Regular ACL audits with BloodHound / PingCastle  
✔ Monitor AD logs via SIEM correlation rules  
✔ Add privileged users to Protected Users group  

---
###  Full Blog
[https://medium.com/@diyatk01/the-silent-war-inside-active-directory-10-attack-methods-soc-teams-miss-a7184c10f407]

