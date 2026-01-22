Homework: Kill Chain
Hutchins et al. (2011): Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains

Abstract
The paper argues that traditional security tools (antivirus, IDS, patching) mainly focus on vulnerabilities, not on the adversary, which makes them ineffective against long‑term, well‑resourced APT actors.
APTs conduct multi‑year, targeted campaigns aimed at stealing sensitive information, often bypassing conventional defenses through custom malware, social engineering, and zero‑day exploits.
The authors propose intelligence‑driven defense, where defenders continuously collect and reuse indicators from intrusions to build a feedback loop that strengthens detection and mitigation over time.
By analyzing intrusions as phased processes rather than isolated incidents, defenders can disrupt attacks earlier and force adversaries to spend more resources adapting.
The approach shifts security from reactive to proactive by addressing not only vulnerabilities but also the threat component of risk.

My question/insight
How realistic is it for smaller organizations to maintain this kind of intelligence cycle? The model seems powerful, but it also assumes a level of analytical capacity that many companies simply don't have.

3.2 Intrusion Kill Chain - Summary
The authors adapt the military "kill chain" concept to cyber intrusions, breaking an attack into seven linked phases.
The key idea is that attackers must succeed in every phase, while defenders only need to break one link to stop the intrusion.
The seven phases are:
Reconnaissance: attacker researches targets, gathers emails, technologies, relationships.
Weaponization: malware is paired with an exploit to create a payload (often PDFs or Office files).
Delivery: payload is sent via email, malicious websites, or removable media.
Exploitation: exploit triggers on the victim system, often through software vulnerabilities or user actions.
Installation: malware/backdoor is installed to maintain persistence.
Command & Control (C2): compromised host connects back to an attacker‑controlled server for remote control.
Actions on Objectives: attacker finally performs their goal - usually data theft, lateral movement, or system misuse.
The model helps defenders understand where their controls are strong or weak and how to disrupt attacks earlier in the chain.

My question/insight
Do modern cloud‑based attacks still follow this linear sequence? Some identity‑based attacks seem to skip several phases entirely, which makes me wonder how the kill chain adapts to newer threat models.

Reference: 
Hutchins, E., Cloppert, M., & Amin, R. (2011). Intelligence‑Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains.  
https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf


Task a) Tactics, Tools and Procedures
Tactic Definition:
A tactic represents the why - the adversary's goal or objective during a specific stage of an intrusion.
Example Tactic (different from kill chain examples):
Defense Evasion The attacker's goal is to avoid detection by security tools or analysts.

Technique Definition:
A technique describes the how - the general method an adversary uses to achieve a tactic.
Example Technique:
Obfuscated/Encrypted Payloads (T1027) Attackers hide malicious code by encrypting or packing it to bypass detection.

Subtechnique Definition:
A subtechnique is a more specific variation of a technique, describing the behavior in finer detail.
Example Subtechnique:
T1027.002 - Software Packing The attacker uses packers to compress or wrap malware so its code is hidden until runtime.

Procedure Definition:
A procedure is the exact, real‑world implementation of a technique or subtechnique. It is what a specific threat actor actually did in the wild.
Example Procedure:
An adversary uses UPX (a common packer) to compress a malware executable before distributing it, allowing it to bypass static antivirus scanning.
This is a concrete, observed action - not just a general technique.

My Questions / Thoughts
ATT&CK is extremely detailed - how do organizations decide which techniques to prioritize when building detections?
Could ATT&CK be used as a maturity model, where defenders measure how many techniques they can detect or mitigate?
Since ATT&CK is updated bi‑annually, how quickly do new real‑world techniques get added after they appear in the wild?

Reference:
MITRE ATT&CK Matrix for Enterprise — https://attack.mitre.org/
MITRE ATT&CK FAQ (General) — https://attack.mitre.org/resources/faq/#general-faq

Task c) Voluntary Bonus: Attack Story
Attack Scenario: Compromise of a Small Design Agency
A mid-sized design studio becomes the target of an attacker who wants to steal the project files of the firm's clients. The attacker employs social engineering, privilege escalation, and stealthy exfiltration.
Below attack flow with tactics, techniques, and procedures according to MITRE ATT&CK.

1. Initial Access
Technique: T1566.002 – Spearphishing Link  
The scammer then sends an email that is tailored to the victim, posing as a client who wants some modifications to a given design on an emergency basis
Procedure: The email contains a malicious link to a false Adobe Cloud webpage.
Credentials are entered by the employee, which are then harvested and submitted to the attacker’s server.
2. Execution
Technique: T1059.001 – PowerShell  
With the acquired credentials, the attacker remotely logs in and runs the PowerShell command.
Procedure: A PowerShell one-liner is used for the download and execution of a lightweight backdoor from a remote server.
3. Persistence
Technique: T1547.001 – Registry Run Keys / Startup Folder
Procedure: The backdoor adds a registry key under:
HKCU\Software\Microsoft\Windows\CurrentVersion\Run  
so it launches automatically at every login.
4. Privilege Escalation
Technique: T1068 - Exploit for Privilege Escalation
Procedure: The attacker exploits a known but unpatched Windows driver vulnerability to gain SYSTEM‑level access.
5.Defense Evasion
Technique: T1027 – Obfuscated/Enc
Procedure: The malware packer makes use of UPX to avoid static antivirus detection.
6. Credential Access
Technique: T1003.001 - LSASS Memory Dump
Procedure: The attacker will use procdump.exe to grab LSASS and additional domain credentials.
7. Lateral Movement
Technique: T1021.002 - SMB/Windows admin
Procedure: Using the newly acquired credentials, the perpetrator continues to the company’s file server.
8. Collection
Technique: T1560 – Archive Collected Data
Procedure: The attacker will then compress all of the project files into a zip file. The zip file will be 
9. Exfiltration 
Technique: T1567.002 Exfiltration Over Web Services 
Procedure: The ZIP file would be transferred to an attacker-controlled Dropbox, using the Dropbox API. 
10. Command and Control
Technique: T1071.001 – Web Prot 
Procedure: The backdoor connects to the server through HTTPS, which makes it look like regular network traffic.

Defensive Actions
Email filtering prevents future spear phishing attacks.
EDR, which detects suspicious PowerShell activity.
Abnormal outbound connections to Dropbox are detected by network monitoring.
Incident response team isolates the compromised workstation and file server.
Patching policy also gets updated to prevent privilege escalations resulting from old drivers.
The awareness level regarding user involvement in these activities continues to be enhanced to prevent phishing attacks.
The intrusion is finally detected through exfiltration, and before additional data is accessed, the attacker’s access is terminated.

References:
These references support the ATT&CK techniques and real‑world behaviors used in the story:
References (Authentic, Publicly Verifiable Sources)
These references support the ATT&CK techniques and real‑world behaviors used in the story:

MITRE ATT&CK - Spearphishing Link (T1566.002) https://attack.mitre.org/techniques/T1566/002/ 
MITRE ATT&CK - PowerShell (T1059.001) https://attack.mitre.org/techniques/T1059/001/ 
MITRE ATT&CK - Registry Run Keys (T1547.001) https://attack.mitre.org/techniques/T1547/001/ 
MITRE ATT&CK - Exploitation for Privilege Escalation (T1068) https://attack.mitre.org/techniques/T1068/
MITRE ATT&CK - Obfuscated/Encrypted Payloads (T1027) https://attack.mitre.org/techniques/T1027/
MITRE ATT&CK - LSASS Credential Dumping (T1003.001) https://attack.mitre.org/techniques/T1003/001/
MITRE ATT&CK - SMB/Windows Admin Shares (T1021.002) https://attack.mitre.org/techniques/T1021/002/
MITRE ATT&CK - Archive Collected Data (T1560) https://attack.mitre.org/techniques/T1560/
MITRE ATT&CK - Exfiltration Over Web Services (T1567.002) https://attack.mitre.org/techniques/T1567/002/
MITRE ATT&CK - Web Protocols (T1071.001) https://attack.mitre.org/techniques/T1071/001/
