# Going Dark - Week 7
**Disclaimer:** In Finland, using TOR is legal at the time of writing.

---

## Reading Summaries

### **Quintin (2014) - *7 Things You Should Know About Tor***

- Tor still offers strong anonymity, even when facing sophisticated surveillance systems.
- It isn't a tool used only by criminals-journalists, activists, researchers, and everyday people rely on it for privacy and protection.
- The project has no hidden government backdoor. Its open‑source code is constantly reviewed by independent experts.
- Running a Tor relay is legal in the U.S., though operating an exit node can attract attention from law enforcement.
- Tools like the Tor Browser and Tails OS make anonymous browsing accessible to non‑technical users.
- Tor has improved in speed over the years, but it still can't match the performance of regular browsing.
- It's not a perfect shield-users still need good privacy habits to stay anonymous.

#### **Reflection**
Reading this made me realize how many ordinary people depend on Tor for safety and privacy.
Its open‑source nature adds a layer of trust, since anyone can inspect the code.
It also highlighted how much information regular browsers leak without us noticing.
I found it reassuring that simply using Tor isn't illegal, even if some people associate it with suspicious behavior.

**Source:** Quintin, C. (2014). *7 Things You Should Know About Tor*. Electronic Frontier Foundation.



### **Shavers & Bair (2016) - *Hiding Behind the Keyboard: The Tor Browser***

#### **Introduction**
Tor is essentially a privacy‑focused version of Firefox designed to hide a user's real IP address.
It's free, easy to use, and doesn't require technical expertise, which is why it's considered one of the most effective tools for private communication.

#### **History and Intended Use**
- Originally developed by the U.S. government in 2002 to protect sensitive communications.
- Intended for legitimate uses such as bypassing censorship, whistleblowing, and securing confidential business discussions.
- Like any technology, it can be misused for illegal purposes.
- Today, Tor is maintained by a global open‑source community rather than any single government.

#### **How The Onion Router Works**
- Traffic passes through at least three volunteer‑run relays: Entry, Middle, and Exit.
- Data is wrapped in multiple layers of encryption-like peeling an onion.
- Each relay removes only one layer and knows only the previous and next hop.
- The Exit relay connects to the final destination but cannot identify the original user.
- Tor automatically changes the route every 10 minutes to strengthen anonymity.

#### **Tracking Criminals on Tor**
Law enforcement rarely breaks Tor itself. Instead, they focus on user mistakes.
Common investigative methods include:

- Exploiting browser vulnerabilities (e.g., injecting malware to reveal IP addresses).
- Social engineering-sending malicious links or files to force a real IP leak.
- Linking online behavior to a suspect's identity through open‑web activity.
- Checking who on a specific network was using Tor at the exact time a threat or message was sent.

#### **Reflection**
It's impressive that a single piece of software can provide such strong anonymity.
The onion‑layer analogy made the cryptography much easier to understand.
I found the relay system clever-no single node ever sees the full picture.
The reading reinforced that human error is the biggest weakness; Tor is only as secure as the person using it.
I was also surprised that most successful investigations rely on traditional detective work rather than breaking Tor itself.

**Source:** Shavers, B. & Bair, J. (2016). *Hiding Behind the Keyboard*. Syngress.

---

# Task A - Installing and Accessing Tor

## Installation Process

I completed the setup using a Debian virtual machine, installing the Tor service directly on the system and routing Firefox traffic through a SOCKS v5 proxy. 
The process was more hands‑on than using the Tor Browser, but it gave me a clearer sense of how the service operates under the hood.

### **Steps Completed**

1. **Updated Debian packages**
```bash
sudo apt update
```

2. **Installed the Tor service**

```bash
sudo apt install tor -y
```

3. **Started the Tor daemon**

```bash
sudo service tor start
```

<img width="524" height="95" alt="h7_taska_1" src="https://github.com/user-attachments/assets/4d0de537-8b7a-4300-a626-a69ee675e94f" />


4. **Configured Firefox to use Tor**

Opened Settings -> Network Settings -> Manual Proxy Configuration

Entered:

 - SOCKS Host: 127.0.0.1

 - Port: 9050

 - SOCKS v5 enabled

 - DNS over SOCKS enabled to prevent DNS leaks
   
Clearly visible in the below screenshot: 

<img width="365" height="131" alt="h7_taska_2" src="https://github.com/user-attachments/assets/a9a05b70-9454-4cef-8831-14fbc76cb600" />

5. **Verified the connection**

Then I visited the Tor check page to confirm that traffic was being routed through the Tor network, also shown in the following screenshot:

<img width="508" height="119" alt="h7_taska_3" src="https://github.com/user-attachments/assets/fc6ed36e-74d4-415e-b300-6d01b9714653" />

#### Reflection
I expected this method to be more complicated, but once the proxy settings were in place, everything worked smoothly. 
The biggest difference compared to normal browsing was the increased latency-pages took noticeably longer to load. 
That slowdown made me more aware of the amount of routing and encryption happening behind the scenes. 
Overall, the setup gave me a better appreciation for how Tor functions at the system level rather than just through a browser bundle.

---

# Task B - Exploring Hidden Services

Using the Tor Browser inside my virtual machine, I explored four different categories of `.onion` sites. 
I limited my activity to viewing landing pages only and did not interact with any content.

## 1. Onion Search Engine - Ahmia

<img width="640" height="184" alt="h7_taskb_1" src="https://github.com/user-attachments/assets/c2718400-7f60-410e-b01d-2211e51b5c3a" />

Ahmia is a search engine designed specifically for indexing Tor hidden services. 
Its interface is clean and straightforward, and it actively filters out abusive or illegal material, which makes it one of the more approachable search tools on the Tor network.

**Why it exists on Tor:**
Ahmia provides a way for users to discover hidden services without sacrificing anonymity. 
By operating within Tor, it allows people to search privately while maintaining a privacy‑respecting environment.

## 2. Marketplace Landing Page - MoonClub Marketplace Section

<img width="640" height="305" alt="h7_taskb_2" src="https://github.com/user-attachments/assets/e71d4296-f1bc-402d-a54a-ba72340cf8a0" />

This landing page displayed various marketplace categories within a forum‑style layout. I only viewed the main page and did not open any listings or interact with the site.

**Why it exists on Tor:**
Marketplaces use Tor to offer anonymous access to goods or services while concealing the identities of both visitors and operators. 
The network's design makes it difficult to trace activity back to individuals.

## 3. Forum - DarknetArmy Forum

<img width="640" height="322" alt="h7_taskb_4" src="https://github.com/user-attachments/assets/f1cd0976-f7f9-479d-90c2-b499c2cccf01" />

The forum presents itself as a community focused on hacking, cybersecurity, and underground discussions. 
I viewed only the public front page, which included general categories and announcements.

**Why it exists on Tor:**
Forums like this rely on Tor to give users a space to discuss sensitive or privacy‑related topics without exposing their real‑world identities. 
The anonymity provided by Tor encourages open conversation in areas where people might otherwise hesitate to participate.

## 4. Well‑Known Organization - BBC News Onion Service

<img width="640" height="268" alt="h7_taskb_3" src="https://github.com/user-attachments/assets/953137fd-0d67-4241-baa7-4a0bd4954187" />

The BBC maintains an official onion mirror of its news site. The landing page closely resembles the regular BBC website, offering access to news stories and sections.

**Why it exists on Tor:**
The BBC provides an onion service to ensure that people in regions with heavy censorship can still access independent journalism. 
Hosting a Tor mirror helps bypass restrictions and keeps information available to audiences who might otherwise be blocked.

#### References

utmapp (2024). *Tails emulated VM with UTM · utmapp/UTM · Discussion #6261*. GitHub. Available at: utmapp/UTM#6261 [Accessed 30 Sep. 2025].

way (2012). *Ask Ubuntu*. Ask Ubuntu. Available at: https://askubuntu.com/questions/166832/is-there-a-way-to-use-tor-system-wide [Accessed 30 Sep. 2025].

---

# Voluntary Task E - Crypto Hunter: Tracking a Bitcoin Address

This task involved locating a Bitcoin donation address on a hidden service and tracing its activity using a public blockchain explorer. 
The goal was to see how cryptocurrency transactions remain visible even when the address originates from a Tor‑based site.

## 1. Finding the Address

While browsing a privacy‑oriented hidden service, I came across a donation page that listed multiple cryptocurrency options. 
The site provided both Bitcoin and Monero addresses. For this task, I chose to analyze the Bitcoin address.

<img width="558" height="228" alt="h7_taske_1" src="https://github.com/user-attachments/assets/8af43cc3-9d71-4e21-b353-d7a859306cd5" />

### **Bitcoin Address Found**

**bc1quuv5383d9cp44wz9lz0mc0wa7mhr2mkzswn2vh**

## 2. Checking the Public Ledger

Using a regular browser outside of Tor, I opened a public blockchain explorer and pasted the address into the search bar. 
The explorer immediately displayed the full transaction history associated with the address.

## 3. Results
The address had been used previously and showed a small but complete transaction history as also shown in the below screenshot:

### **Transaction Summary**
- **Confirmed Transactions:** 2
- **Total Received:** 0.00056868 BTC
- **Total Spent:** 0.00056868 BTC
- **Current Balance:** 0 BTC

The activity shows that the address received funds and later spent the entire amount.

<img width="1314" height="762" alt="h7_taske_2" src="https://github.com/user-attachments/assets/e59b10a5-6eb6-41a6-b68b-bf24b1088e48" />

## 4. Interpretation

The presence of real transactions suggests that the donation address is legitimate rather than a placeholder. 
Even though the site operates on the darknet, the Bitcoin blockchain remains fully transparent. Tor can hide who is visiting the site, but it cannot hide the movement of funds. 
Every transaction is permanently recorded on the public ledger.

This contrast highlights an interesting dynamic: Tor provides anonymity for browsing, while Bitcoin exposes financial activity to anyone who knows the address.

## 5. Reflection

This task was more revealing than I expected. I assumed darknet donation addresses might be inactive or difficult to trace, but the blockchain explorer made everything completely visible. 
Seeing the full transaction history emphasized how anonymity and transparency can coexist in unexpected ways. Tor protects identity, but Bitcoin preserves every transaction forever.

#### Reference
blockstream.info. (n.d.). *Bitcoin Explorer*. Available at: https://blockstream.info/.

---

## Conclusion

Working through this assignment gave me a clearer understanding of how Tor functions, how hidden services operate, and how anonymity tools interact with public systems like blockchains. 
The experience showed both the strengths and limitations of privacy technologies. 
Tor is effective at anonymizing browsing, but it doesn't erase traces when interacting with transparent systems such as Bitcoin. 
Overall, the tasks reinforced the importance of good OPSEC and awareness of how different technologies overlap.
