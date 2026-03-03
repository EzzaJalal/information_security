# February2026! - Week 6

---
## Schneier 2015: Applied Cryptography

### 2.3 One‑Way Functions

A **one‑way function** is a function that is easy to compute in one direction but extremely difficult to reverse.
You can quickly calculate \( f(x) \) from \( x \), but determining \( x \) from only \( f(x) \) would require an unrealistic amount of computing power, even if every computer in the world worked together.
There is no formal proof that true one‑way functions exist, but many strong candidates behave this way in practice.
On their own, they **cannot** be used as encryption mechanisms, because no one would be able to recover the original message.
A **trapdoor one‑way function** solves this by adding a secret piece of information - the *trapdoor* - that makes reversing the function easy for whoever holds that secret.

#### My thoughts
This section lays out the basic idea behind modern encryption. One‑way functions act like the "locks," and the trapdoor element serves as the "key" that enables public‑key systems to work.

---

### 2.4 One-Way Hash Functions

A **one‑way hash function** takes input of any length and produces a fixed‑size output, known as a *hash*.
It acts like a digital fingerprint: even a tiny change in the input results in a completely different hash.

"One‑way" means:
- It's simple to compute the hash.
- It's extremely hard to recover the original input.
- It's extremely hard to find another input that produces the same output (a *collision*).

Hashing does **not** rely on secrecy; its security comes from the mathematical difficulty of reversing or manipulating the function.
This makes hashes ideal for verifying data integrity without needing to transmit the entire dataset.
A **Message Authentication Code (MAC)** adds a secret key to the hashing process so that only someone with the key can confirm the authenticity of the data.

#### My thoughts
Hashes function like digital fingerprints. They're incredibly useful for checking integrity and authenticity, even though they don't provide secrecy on their own.

##### Reference
Schneier, B. and Diffie, W. (2015). *Applied Cryptography: Protocols, Algorithms, and Source Code in C.* Indianapolis (Ind.): Wiley.

---

## a & b) Installing Hashcat, Testing with a Sample Hash and Cracking a Hash

I began by reviewing Tero Karvinen's article on Hashcat to understand how password‑cracking tools operate and why hashed passwords can be recovered through dictionary attacks. Before running any commands, I made sure I understood the role of **hash modes**, **wordlists**, and the general workflow Hashcat follows.

To set up the environment, I installed Hashcat on my Linux system using:

### Installation and Setup

The work was performed inside a **Debian virtual machine**. The required tools were installed using the system package manager:

```bash
sudo apt update
sudo apt -y install hashcat hashid wget
```

A dedicated working directory was created to keep everything organized:

```bash
mkdir hashlab
cd hashlab
```
The RockYou wordlist, commonly used in password‑cracking exercises due to its size and real‑world passwords, was downloaded and extracted by using the following commands:

```bash
wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz
tar xf rockyou.txt.tar.gz
rm rockyou.txt.tar.gz
```
### Hash Identification
The target hash for this task was:
**d595b2086532422bbe654bc07ea030df**

Before cracking, I identified the hash type by using hashid:

```bash
hashid -m d595b2086532422bbe654bc07ea030df
```
The output indicated that the hash matches the MD5 format, which corresponds to Hashcat mode 0.

**<img width="425" height="193" alt="h6_taska b_1" src="https://github.com/user-attachments/assets/9078eb47-0746-426f-984c-8455d1cf4329" />**

It showed possible types like:
- MD2
- MD5
- MD4

A file was created to store the hash:

```bash
echo "d595b2086532422bbe654bc07ea030df" > target.hash
```

### Cracking the Hash
I ran Hashcat using MD5 mode because it is the most common and the RockYou dictionary:

```bash
hashcat -m 0 target.hash rockyou.txt -o cracked.txt
```

**<img width="640" height="111" alt="h6_taska b_2" src="https://github.com/user-attachments/assets/c792fc7e-dca7-4285-bcba-13c258644da5" />**

After the attack completed, the result was inspected:

```bash
cat cracked.txt
```
This revealed the plaintext password associated with the hash as shown in the below screenshot:

**<img width="257" height="36" alt="h6_taska b_3" src="https://github.com/user-attachments/assets/5958f8d8-0df8-42ec-abc8-4545f1b131f0" />**

Verification
I confirm the result, Hashcat's --show option was used as below:

```bash
hashcat -m 0 target.hash rockyou.txt --show
```
This displayed the hash and its corresponding cracked password, verifying that the attack succeeded.
Hash cracked, this means the hash was successfully cracked.


### What I Learned

- Taking the time to understand the concepts behind the process made a big difference.
- If I had simply copied steps from a tutorial, I would not have appreciated why some hash types take dramatically longer to break than others.
- I also realized that relying on raw computing power alone isn't the smartest approach.
- Using focused dictionary attacks and rule‑based methods can cut the cracking time by a huge margin.
- This exercise also reinforced why MD5 is no longer considered secure-it's far too fast and easy to brute‑force.
- It became clear that using long, unique passwords is one of the most effective ways to defend against these kinds of attacks.

##### Source
Terokarvinen.com (2022). Cracking Passwords with Hashcat. Available at: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/ (Accessed 6 Oct. 2025).

---

## p) Voluntary - Forbes 2019: Jackpotting ATMs (Automated Teller Machines)

Modern ATMs turn out to be far less secure than most people assume.
They're essentially regular Windows machines with a few extra components attached, and the entire market is controlled by just four major manufacturers: Diebold Nixdorf, NCR, Siemens, and Hitachi.
Physical protection is surprisingly weak, with universal keys easy to buy online and locks that offer little resistance.
Many ATMs rely on XFS middleware, which makes it possible for attackers to create portable tools that work across different brands.

There are several common attack methods, including gaining physical access through weak locks or forcing open the casing.
Network‑based attacks are also widespread, especially since nearly 30% of machines don't properly authenticate their backend connections.
Hard‑drive swapping is another frequent tactic because full disk encryption is rarely enabled. Black‑box attacks allow criminals to connect external devices directly to the cash dispenser, and man‑in‑the‑middle setups can intercept or manipulate network traffic.

The talk highlighted a number of serious security gaps: default passwords are still common, software is outdated and seldom patched, and many machines rely on cheap networking equipment with poor security.
Less than 10% of ATMs use full disk encryption, and physical installation is often done poorly.
While most cash theft still relies on brute force, more advanced attackers target backend systems to bypass withdrawal limits.
Malware families exist that work across multiple ATM brands, and many attacks begin by collecting card data before moving on to cash‑out operations.

Defense recommendations included enabling full disk encryption with TPM support, improving physical installation, segmenting networks, using proper firewalls, keeping systems patched, enforcing application whitelisting, and requiring mutual authentication between all components.

### My Reflection

What stood out to me most was how much trust people place in ATM security compared to how little protection actually exists. It was surprising to learn that these machines run on basic Windows setups with minimal hardening, and that universal keys can be bought without difficulty. The lack of full disk encryption on such critical systems shows how fundamental security practices are often ignored.

Because so many ATMs share the same architecture, a single successful attack can be replicated worldwide. It's a reminder that physical and digital security are deeply connected-weak locks can undermine even the strongest technical safeguards. The biggest concern, though, is the mindset around ATM maintenance. These systems are treated as if they should be left alone as long as they function, instead of being viewed as high‑risk targets that require continuous security improvements. The talk made it clear that widespread vulnerabilities often come from basic oversights rather than sophisticated exploits.

##### Source
Disobey (2019). *Jackpotting ATM's (Automated Teller Machines) - It's easier than you might think* - Alexander Forbes. YouTube. https://www.youtube.com/watch?v=ThPJrPf7O2s (Accessed 6 Oct. 2025).
