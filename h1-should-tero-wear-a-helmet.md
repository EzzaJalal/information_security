Should Tero Wear a Helmet?
Threat Modeling Manifesto (Braiterman et al., 2020)
Threat modeling assists in understanding a system to effectively identify security and privacy concerns.
The manifesto emphasizes ideas such as cooperation, people-centric thinking, and a commitment to continuous improvement.
It also establishes principles such as the use of structured methods, fostering informed creativity, and representing varied perspectives.
Anti-patterns include a warning about placing too much emphasis on a “single expert,” getting “stuck in analysis,” or “losing sight of the big picture.”
Thought: Creativity is encouraged, but it is hard to gauge. How do you remain creative and not get lost in brainstorming?

Shostack – World’s Shortest Threat Modeling Course (2022)
Threat modeling is more efficient before code is written or when an inexpensive change can be made.

Interview questions:The Four Questions:
What are we working on?
What can go wrong?
What are we going to do about it?
Were we doing a good job?

One of the reasons why data flow diagrams are useful is because "threats follow data, not organizational charts."
Diagrams of flow contain 5 symbols:
External factors: outside our control (sharp pointy corners)
Processes: Any code executing in our controlled environment
Data Flows: The component that ties together entities and processes.
Data Stores, where data is stored (drunms)
Trust boundaries: where we demonstrate how different components are controlled by different actors.

STRIDE offers an organized approach to make sure threats aren’t missed.
Thought: "The ‘Would you recommend this project to a friend?’ test is surprisingly effective – it highlights things which may have been missed by formal checklists."

OWASP Threat Modeling Cheat Sheet (2021)
Intended Benefits:
Early risk detection
Improved security awareness
Better understanding of system behavior

Issues:
Limited security expertise
Time pressure
Communication gaps between teams

Suggested improvements:
Regular training
Involving security experts
Using Automation Wisely
Building long‑term security culture
Thought: Automation is great, but if teams rely on it too much, then they may miss subtle or context‑specific threats.

Darknet Diaries - Episode 66: The Police Station Incident
A ransomware attack has hit a small‑town U.S. police station, locking officers out of critical systems.
The attackers demanded payment in Bitcoin, and the department was in distress with no easy way out since they had no backups nor good security hygiene.
The incident showed how several public institutions are underfunded, sometimes even more so in the area of cybersecurity.
Officers had to revert to pen‑and‑paper operations, slowing down response times in emergency situations.
Eventually, the department relented to pay the ransom-a decision shrouded in controversy for ethical and legal reasons.
Thought: Cybersecurity failure causing danger to the life of people is not just about data or money.

a) Security Hygiene
Basic Practices Everyone Should Know
Utilize strong, unique passwords or a password manager
Enable multi‑factor authentication
Keep devices and software up-to-date
Be careful with links and attachments
Encrypt devices
Backup important data
Avoid using public Wi‑Fi without a VPN

Company‑Level Practices
Segmentation of a Network
Automatic patching
Backup regularly and test its recovery.
Security awareness training
Incident response planning Regular audits and penetration testing

b) Make‑Belief Boogie‑Man — Threat Model for an Imaginary Company
Threat Model for AuroraRide
AuroraRide is a hypothetical electric‑scooter rental firm working in most major European cities. Its customers unlock scooters with a mobile app, and its business relies heavily on real‑time GPS data, payment processing, and fleet management systems.

(1) What Are We Working On?
Key Assets (Prioritized)

Asset	                      Priority	                               Reason
Rider location data	          High	                   Sensitive, real‑time tracking of individuals
Payment information    	      High	                   Financial risk and fraud potential
Fleet GPS & battery data	    Medium	                 Needed for operations, not personally sensitive
User accounts	                Medium	                 Important for service continuity
Scooter hardware	            Low	                     Physical loss is manageable

Customer Touchpoints
Mobile app
Website
Email notifications
QR code scanner on scooters
Customer support chat

System Diagram

<img width="1567" height="804" alt="Screenshot 2026-01-17 225444" src="https://github.com/user-attachments/assets/1ed22373-a9f9-456e-b10b-4fc95cba2dd7" />

AuroraRide must ensure scooters are available, payments are secure, and location data is protected — otherwise customers lose trust and stop using the service.

(2) What Can Go Wrong?
Applied Models
STRIDE
CIA Triad
MITRE ATT&CK

Example Threats
GPS spoofing → attacker controls scooter location data (Integrity)
Account take over via phishing (Spoofing)
API misuse → mass unlocking of scooters (Elevation of Privilege)
Payment fraud-the app uses stolen cards. [Financial risk] 
DoS attack on fleet servers → scooters become unavailable Availability

Risk Prioritization Table
Threat	            Probability	     Impact	      Priority
Payment fraud	        Medium	      Very High	     Critical
GPS spoofing	        Low	          High	         High
Account takeover	    Medium	      High	         High
DoS attack	          Medium	      Medium	       Medium
Insider misuse	      Low	          Medium	       Low

Threat Actors
Cyber Criminals Targeting Payment Systems
Rivals looking for operations information
Hacktivists campaigning against e-scooters in
Insiders with Privileged Access

Known TTPs
Credential Stuffing
Api scraping
GPS spoofing software
Bot-operated DoS Attacks

Business Continuity 
AuroraRide needs its scooters to remain in working condition, as any downtime impacts its revenues. Consumer trust is delicate; an incident related to privacy can hurt the trademark.

(3) What Are We Going To Do About It?
META Framework


Action Type	                     Controls
Mitigate	        MFA, rate limiting, GPS anomaly detection, encryption, API throttling
Eliminate	        Remove unused admin endpoints, disable outdated scooter firmware
Transfer	        Use third‑party payment processors
Accept	          Minor scooter vandalism (low financial impact)

(4) Did We Do a Good Enough Job?
Continuous Evaluation
Besides
Routine penetration tests
Security audits
Monitorization of scooter telemetry
Incident response drills
Maintaining the threat model with new features that come out
“Security is an ongoing process, and as the attackers evolve, so must AuroraRide,” said the spokesperson.

References
Threat Modeling Manifesto
https://www.threatmodelingmanifesto.org/

Shostack – World’s Shortest Threat Modeling Course
https://www.youtube.com/playlist?list=PLCVhBqLDKoOOZqKt74QI4pbDUnXSQo0nf (youtube.com in Bing)

OWASP Threat Modeling Cheat Sheet
https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html (cheatsheetseries.owasp.org in Bing)

Darknet Diaries – Episode 66
https://darknetdiaries.com/episode/66/

MITRE ATT&CK Framework
https://attack.mitre.org/

Karvinen, T. (2024). Information Security Course
https://terokarvinen.com/information-security/


