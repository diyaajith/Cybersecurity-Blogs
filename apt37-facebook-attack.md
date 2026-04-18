##  When a Facebook Friend Request Becomes a Cyber Trap

**Threat Actor:** APT37 (ScarCruft)  
**Focus:** Social Engineering • Malware Delivery • Threat Intelligence  

---

###  Overview
This write-up analyzes a targeted campaign where North Korean threat actors leveraged social media platforms like Facebook and Telegram to deliver malware through highly convincing social engineering techniques.

Instead of exploiting software vulnerabilities, the attack relied on **human trust** — guiding victims from a simple friend request to installing a trojanized PDF viewer that ultimately deployed the **RokRAT Remote Access Trojan**.

---

###  Key Attack Techniques
- **Pretexting & Social Engineering:** Fake personas used to build trust across platforms  
- **Trojanized Software:** Modified PDF viewer (Wondershare PDFelement) used as initial payload  
- **Steganography:** Malicious payload hidden inside a `.jpg` file  
- **Living-off-the-Land C2:** Abuse of Zoho WorkDrive for stealthy command & control  

---

###  Malware Breakdown — RokRAT
- Modular Remote Access Trojan used for espionage  
- Data exfiltration (files, screenshots, system info)  
- Encrypted communication with cloud-based C2  
- Designed for persistence and low detection  

---

###  MITRE ATT&CK Mapping
- **T1566** – Phishing (Initial Access)  
- **T1204** – User Execution  
- **T1036** – Masquerading  
- **T1102** – Web Services (C2 via cloud platforms)  
- **T1027** – Obfuscation  
- **T1113** – Screen Capture  

---

###  Defensive Insights (NIST CSF)
- **Identify:** Lack of awareness around social engineering vectors  
- **Protect:** Weak application control policies  
- **Detect:** Need for behavioral monitoring over signature-based detection  
- **Respond:** Delayed detection due to low-noise malware  
- **Recover:** Requires deep forensic analysis due to persistence mechanisms  

---

###  Key Takeaway
This attack highlights a critical shift:

> The entry point is no longer just vulnerable systems — it's human behavior.

No zero-day exploit. No brute force.  
Just trust, manipulation, and a seemingly harmless file.

---

###  Full Blog
[https://medium.com/@diyatk01/when-a-facebook-friend-request-becomes-a-cyber-trap-how-north-korean-hackers-are-using-social-1c634481d2f4]
