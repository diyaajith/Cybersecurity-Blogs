## Defense Evasion at Kernel Level: Qilin & Warlock Ransomware (BYOVD Analysis)

**Threat Type:** Ransomware  
**Techniques:** BYOVD • DLL Side-Loading • Defense Evasion • Privilege Escalation  
**Focus:** Detection Engineering • SOC Analysis • Threat Intelligence  

---

###  Overview
This write-up examines how modern ransomware groups such as Qilin and Warlock are shifting tactics by prioritizing **defense evasion before encryption**.

The campaign leverages **Bring Your Own Vulnerable Driver (BYOVD)** techniques to gain **kernel-level (Ring 0) execution**, allowing attackers to disable over 300 security tools and bypass traditional endpoint protections.

Rather than exploiting zero-day vulnerabilities, this approach abuses **legitimately signed but vulnerable drivers**, making detection significantly more challenging.

---

### Technical Breakdown

####  Initial Access
- Use of stolen credentials or exploitation of exposed services  
- Attackers operate under legitimate user context early in the intrusion  

####  Execution via DLL Side-Loading
- Malicious `msimg32.dll` is loaded through trusted applications  
- Exploits Windows DLL search order to execute attacker-controlled code  

**Detection Clues:**
- DLLs loaded outside:
  - `C:\Windows\System32\`
  - `C:\Windows\SysWOW64\`
- Execution from user/temp directories  

---

####  Multi-Stage Payload Delivery
- **Stage 1:** Loader initializes execution  
- **Stage 2:** Encrypted payload decrypted and executed in memory  

 Reduces disk artifacts and evades signature-based detection  

---

####  Defense Evasion
- Suppression of **Event Tracing for Windows (ETW)**  
- Removal or bypass of monitoring hooks  
- Obfuscation of execution flow  

 Results in reduced visibility across EDR and logging systems  

---

####  BYOVD (Kernel-Level Abuse)
Attackers deploy vulnerable drivers to gain **Ring 0 execution**, enabling:

- Direct memory manipulation  
- Termination of protected security processes  
- Removal of kernel callbacks used by EDR tools  

**Drivers Observed:**
- `rwdrv.sys` — Direct physical memory access  
- `hlpdrv.sys` — Process termination capabilities  
- `NSecKrnl.sys` — Kernel-level manipulation  

---

####  Impact Phase
- Termination of 300+ security tools  
- Loss of endpoint telemetry and monitoring  
- Delayed ransomware deployment to expand attack surface  

---

###  Warlock Campaign Observations
Warlock operations complement this approach with:

- Exploitation of unpatched services (e.g., SharePoint)  
- Lateral movement using tools like **PsExec**  
- Data exfiltration via **Rclone**  
- Command-and-control via tunneling tools  
- Persistent access through remote utilities  

Ransomware execution is often delayed by days, enabling deeper compromise  

---

###  MITRE ATT&CK Mapping
- **T1574.002** — DLL Side-Loading  
- **T1068** — Privilege Escalation (Vulnerable Driver Abuse)  
- **T1562.001** — Impair Defenses  
- **T1070** — Indicator Removal  

---

###  Detection Strategy

Focus on **behavioral anomalies**, not just signatures:

- Unexpected driver installations or loads  
- Drivers executed from non-standard paths  
- Sudden termination of multiple security processes  
- Loss of telemetry or logging inconsistencies (ETW gaps)  
- Suspicious DLL loading patterns  
- Indicators of lateral movement or abnormal outbound traffic  

---

###  Indicators of Compromise (IOCs)
- `msimg32.dll` outside standard system directories  
- `rwdrv.sys`  
- `hlpdrv.sys`  
- `NSecKrnl.sys`  

 Presence in unusual locations = **high-confidence indicator of compromise**

---

###  Mitigation & Hardening
- Enable **Microsoft vulnerable driver blocklist (WDAC)**  
- Restrict driver loading to trusted and signed publishers only  
- Monitor driver installation and kernel module loading events  
- Enforce least privilege access controls  
- Maintain regular patching cycles  
- Implement behavior-based detection (EDR/XDR)  

---

###  Key Takeaways
- BYOVD enables attackers to operate at **kernel level**, bypassing security tools  
- Defense evasion is now a **pre-encryption phase** in ransomware attacks  
- Traditional detection methods are insufficient without behavioral analysis  
- Driver monitoring is critical for early detection  

---

###  Conclusion
This campaign reflects a broader evolution in ransomware tradecraft:

> **Disable defenses first. Encrypt later.**

Understanding and detecting **kernel-level abuse and pre-ransomware activity** is essential for modern SOC operations and incident response.

---

###  Full Blog
[https://medium.com/@diyatk01/how-qilin-and-warlock-ransomware-disable-300-security-tools-using-vulnerable-drivers-cbbd00c56f75]
