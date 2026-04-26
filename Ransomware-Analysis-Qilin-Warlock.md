
**Defense Evasion at Kernel Level: Qilin & Warlock (BYOVD)**

**Threat Actor:** Qilin & Warlock
**Focus:** Defense Evasion • Privilege Escalation

---

### **Overview**

Ransomware actors now evade defenses *before* encryption using BYOVD—abusing vulnerable signed drivers to gain kernel-level access and disable security tools.

---

### **Key Techniques**

* **BYOVD:** Kernel-level control
* **DLL Side-Loading:** `msimg32.dll` abuse
* **Evasion:** ETW suppression, hook removal
* **Tool Abuse:** PsExec, Rclone

---

### **Impact**

* Disables 300+ security tools
* Enables stealth, persistence, delayed encryption

---

### **Attack Flow**

Access → DLL Side-Load → BYOVD → Lateral Movement → Delayed Ransomware

---

### **MITRE ATT&CK**

T1574.002 • T1068 • T1562.001 • T1070

---

### **Detection Tips**

* Unusual driver loads
* Security tool termination spikes
* ETW/logging gaps
* Suspicious DLL paths

---

### **IOCs**

`msimg32.dll` • `rwdrv.sys` • `hlpdrv.sys` • `NSecKrnl.sys`

---

### **Mitigation**

* Enable driver blocklist (WDAC)
* Restrict driver loading
* Monitor kernel activity
* Use behavior-based detection

---

### **Full Blog**
(https://medium.com/@diyatk01/how-qilin-and-warlock-ransomware-disable-300-security-tools-using-vulnerable-drivers-cbbd00c56f75)
