# Should Tero Wear a Helmet?

## Threat Modeling Manifesto (Braiterman et al., 2020)

- Threat modeling assists in understanding a system to effectively identify security and privacy concerns.
- Emphasizes cooperation, people-centric thinking, and continuous improvement.
- Principles include structured methods, fostering informed creativity, and representing varied perspectives.
- Anti-patterns warn against relying on a “single expert,” getting stuck in analysis, or losing sight of the big picture.

**Thought:** Creativity is encouraged, but it is hard to gauge. How do you remain creative and not get lost in brainstorming?

---

## Shostack – World’s Shortest Threat Modeling Course (2022)

- Threat modeling is more efficient before code is written or when inexpensive changes can be made.
- The Four Questions:
  1. What are we working on?
  2. What can go wrong?
  3. What are we going to do about it?
  4. Did we do a good job?
- Data flow diagrams are useful because **“threats follow data, not organizational charts.”**
- Flow diagram symbols:
  - **External entities** – outside our control  
  - **Processes** – code executing in our environment  
  - **Data Flows** – connect entities and processes  
  - **Data Stores** – where data is stored  
  - **Trust boundaries** – show separation of control  

**Thought:** The “Would you recommend this project to a friend?” test is surprisingly effective — it highlights issues missed by formal checklists.

---

## OWASP Threat Modeling Cheat Sheet (2021)

### Intended Benefits
- Early risk detection  
- Improved security awareness  
- Better understanding of system behavior  

### Issues
- Limited security expertise  
- Time pressure  
- Communication gaps  

### Suggested Improvements
- Regular training  
- Involving security experts  
- Using automation wisely  
- Building long-term security culture  

**Thought:** Automation is great, but over-reliance may cause teams to miss subtle or context-specific threats.

---

## Darknet Diaries – Episode 96: The Police Station Incident

- Nicole Beckwith, a former police officer and Secret Service task force member, responds to a ransomware attack at a small U.S. police department.
- The department believed they restored systems from backups, but later discovered the backups were nearly a year old and had never been tested.
- A week later, the same symptoms reappear — printers failing, systems slowing — prompting Nicole to rush onsite with her forensic go‑bag.
- She performs rapid memory captures and packet analysis using tools like **Volatility** and **Wireshark**.
- Nicole discovers multiple unauthorized admin sessions active on the domain controller, confirming an attacker is inside the network **right now**.
- She kicks out the intruders, resets credentials, and begins deeper forensic analysis.
- The outsourced IT contractor is initially uncooperative despite being responsible for monitoring the network.
- The case highlights how underfunded public institutions struggle with cybersecurity and how misconfigurations (like exposed RDP) can compromise an entire police department.

**Thought:** Cybersecurity failures in essential services can directly impact public safety, not just data or finances.

---

# a) Security Hygiene

## Basic Practices Everyone Should Know

- Use strong, unique passwords or a password manager  
- Enable multi-factor authentication  
- Keep devices and software up-to-date  
- Be cautious with links and attachments  
- Encrypt devices  
- Backup important data  
- Avoid public Wi-Fi without a VPN  

## Company-Level Practices

- Network segmentation  
- Automatic patching  
- Regular backups and recovery testing  
- Security awareness training  
- Incident response planning  
- Regular audits and penetration testing  

---

# b) Make-Belief Boogie-Man — Threat Model for an Imaginary Company

# AuroraRide Threat Model

AuroraRide is a hypothetical electric-scooter rental firm operating in major European cities. Customers unlock scooters via a mobile app. The company relies on real-time GPS data, payment processing, and fleet management systems.

---

# (1) What Are We Working On?

## Key Assets (Prioritized)

| Asset                  | Priority | Reason                                         |
|------------------------|----------|------------------------------------------------|
| Rider location data    | High     | Sensitive, real-time tracking of individuals   |
| Payment information    | High     | Financial risk and fraud potential             |
| Fleet GPS & battery    | Medium   | Needed for operations, not personally sensitive|
| User accounts          | Medium   | Important for service continuity               |
| Scooter hardware       | Low      | Physical loss is manageable                    |

---

## Customer Touchpoints

- Mobile app  
- Website  
- Email notifications  
- QR code scanner on scooters  
- Customer support chat  

---

## System Diagram


<img width="1381" height="750" alt="h1-SystemDiagram-screenshot" src="https://github.com/user-attachments/assets/74450c13-be41-435f-b323-b2a8a2716b1e" />


## AuroraRide System Overview

AuroraRide must ensure scooters are available, payments are secure, and location data is protected — otherwise customers lose trust and stop using the service.

---

## (2) What Can Go Wrong?

### Applied Models
- **STRIDE**
- **CIA Triad**
- **MITRE ATT&CK**

### Example Threats
- **GPS spoofing** → attacker controls scooter location data *(Integrity)*
- **Account takeover via phishing** *(Spoofing)*
- **API misuse** → mass unlocking of scooters *(Elevation of Privilege)*
- **Payment fraud** → stolen cards used in app *(Financial risk)*
- **DoS attack** → scooters become unavailable *(Availability)*

---

### Risk Prioritization Table

| Threat            | Probability | Impact     | Priority |
|-------------------|-------------|------------|----------|
| Payment fraud     | Medium      | Very High  | Critical |
| GPS spoofing      | Low         | High       | High     |
| Account takeover  | Medium      | High       | High     |
| DoS attack        | Medium      | Medium     | Medium   |
| Insider misuse    | Low         | Medium     | Low      |

---

### Threat Actors
- Cybercriminals targeting payment systems  
- Rivals seeking operational data  
- Hacktivists protesting e‑scooters  
- Insiders with privileged access  

---

### Known TTPs
- Credential stuffing  
- API scraping  
- GPS spoofing software  
- Bot‑operated DoS attacks  

---

### Business Continuity
AuroraRide needs its scooters to remain in working condition, as any downtime impacts revenue.  
Consumer trust is delicate; a privacy incident can damage the brand.

---

## (3) What Are We Going To Do About It?

### META Framework

| Action Type | Controls |
|-------------|----------|
| **Mitigate** | MFA, rate limiting, GPS anomaly detection, encryption, API throttling |
| **Eliminate** | Remove unused admin endpoints, disable outdated scooter firmware |
| **Transfer** | Use third‑party payment processors |
| **Accept** | Minor scooter vandalism (low financial impact) |

---

## (4) Did We Do a Good Enough Job?

### Continuous Evaluation
- Routine penetration tests  
- Security audits  
- Monitoring scooter telemetry  
- Incident response drills  
- Updating the threat model with new features  

> “Security is an ongoing process, and as the attackers evolve, so must AuroraRide,” said the spokesperson.

---

## References
- **Threat Modeling Manifesto**  
www.threatmodelingmanifesto.org. (n.d.). Threat Modeling Manifesto. [online] Available at: https://www.threatmodelingmanifesto.org/

- **Shostack – World’s Shortest Threat Modeling Course**  
  Shostack. (n.d.). World’s Shortest Threat Modeling Course. [online] Available at: http://www.youtube.com/playlist?list=PLCVhBqLDKoOOZqKt74QI4pbDUnXSQo0nf

- **OWASP Threat Modeling Cheat Sheet**  
 OWASP Threat Modeling. [online] cheatsheetseries.owasp.org. Available at: https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html

- **Darknet Diaries – Episode 66**  
  Darknet Diaries [online] Available at: https://darknetdiaries.com/episode/96/

- **MITRE ATT&CK Framework**  
  https://attack.mitre.org/

- **Karvinen, T. (2024). Information Security Course**  
  https://terokarvinen.com/information-security/

- **Top Threat Modeling Frameworks**
  Poston, H. (2021). Top threat modeling frameworks: STRIDE, OWASP Top 10, MITRE ATT&CK framework and more | Infosec. [online] www.infosecinstitute.com. Available at: https://www.infosecinstitute.com/resources/management-compliance-auditing/top-threat-modeling-frameworks-stride-owasp-top-10-mitre-attck-framework/.

- **AI Usage**
  AI has been used for the mark down formatting of this report.

- **PowerPoint**
  Powerpoint is used for making the diagrams.


