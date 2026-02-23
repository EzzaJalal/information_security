# Uryyb, Greb! - Week 5

---

## x.1) Schneier 2015 - Applied Cryptography: Chapter 1: Foundations

The shift from plaintext to ciphertext relies on algorithms combined with keys. Cryptography aims to achieve confidentiality, authentication, and integrity. Kerckhoffs's principle states that security must depend on keeping the key secret rather than hiding the algorithm itself. Cryptographic methods fall into two main categories:

- **Symmetric systems**
- **Public‑key systems**

At the lowest level, cryptography works with **bits** rather than characters.

### Attack Models

- Ciphertext‑only
- Known‑plaintext
- Chosen‑plaintext
- Adaptive chosen‑plaintext

Systems can be:

- **Unconditionally secure**, or
- **Computationally secure**

Security difficulty is measured by:

- Required data
- Processing effort
- Storage demands

### Classical vs Modern Cryptography

- Classical ciphers can be broken using frequency analysis.
- XOR encryption is trivial to break despite commercial use.
- One‑time pads provide perfect secrecy when keys are random and never reused.
- Modern algorithms include:
- **DES** (symmetric)
- **RSA** (public‑key)
- **DSA** (digital signatures)

Open algorithms are more trustworthy because they can be publicly examined.

Although one‑time pads offer perfect security, they are impractical for everyday use. Many "new" commercial ciphers are simply weak classical designs repackaged. Real‑world cryptographic strength depends on making attacks computationally infeasible.

Cryptography has evolved from character manipulation to mathematical bit operations. Steganography hides the existence of a message entirely.

### Reflection Question

If one‑time pads provide perfect secrecy but are too inconvenient for everyday use, what does that tell us about the trade‑off between ideal security and what people can realistically adopt?

**Reference:**
CHAPTER 1: Foundations (2025). *Applied Cryptography: Protocols, Algorithms and Source Code in C, 20th Anniversary Edition.*
https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/08_chap01.html#chap01-sec001

---

## x.2) PGP: Sending Encrypted and Signed Messages

- PGP/GPG supports both message encryption and digital signatures.
- Public‑key cryptography makes it possible to communicate securely without sharing a secret key beforehand.
- Public keys are meant to be distributed freely, while private keys must remain confidential.
- Each person generates their own keypair using:

```bash
gpg --gen-key
```
Public keys can then be exported and shared.

### Trust and Verification
- To establish trust, fingerprints must be confirmed through a separate, reliable channel.

When sending a message:
- Sender encrypts with the recipient's public key
- Sender signs with their private key
- Recipient decrypts with their private key
- Recipient verifies the signature using the sender's public key

Key Commands Used:

```bash
gpg --gen-key # Generate keypair
gpg --export --armor --output key.pub # Export public key
gpg --import key.pub # Import others' public keys
gpg --encrypt --sign --recipient user@email.com message.txt # Encrypt & sign
gpg --decrypt encrypted.pgp # Decrypt & verify
```

#### Thoughts & Insights
The most challenging part is building trust. Even strong cryptography is useless if you end up trusting the wrong key.

**Reference:**
Terokarvinen.com (2023). PGP - Send Encrypted and Signed Message - gpg.
https://terokarvinen.com/2023/pgp-encrypt-sign-verify/

---

## a) Install OpenSSH Server & Connect

I started by installing the OpenSSH server on my Debian system. Before installing, I updated the package manager to ensure everything was current. After installation, I enabled the SSH service so it would start automatically on boot.

### Commands Used

```bash
sudo apt install openssh-server -y
sudo systemctl start ssh
sudo systemctl enable ssh
```
**<img width="466" height="37" alt="h5_Taska_1" src="https://github.com/user-attachments/assets/52eba8ac-11e3-4e19-9c4a-6f61d7d6ca1e" />**

The screenshot below shows my first SSH connection to localhost.
As expected, I received a host key verification warning because this was my first time connecting.
I checked the ED25519 fingerprint and accepted it by typing "yes".

**<img width="136" height="36" alt="h5_Taska_2" src="https://github.com/user-attachments/assets/3766777e-530c-4d8b-9534-ca2fef3e17e2" />**

**Tutorial Source:**
DigitalOcean. (n.d.). How To Use SSH to Connect to a Remote Server.
https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server


## b) Automate SSH with Public Keys

To eliminate the need for password authentication, I set up SSH public key authentication.
I generated an **ED25519** SSH key pair and accepted the default storage location.
After that, I copied my public key into the `authorized_keys` file on the remote host using `ssh-copy-id`.

### Commands Used

```bash
ssh-keygen -t ed25519
ssh-copy-id ezzaj@localhost
ssh ezzaj@localhost # Verified passwordless login worked
```
Following screenshots show the successful setup and confirmation that passwordless login was functioning correctly:

**<img width="640" height="189" alt="h5_Taskb_1" src="https://github.com/user-attachments/assets/3cbcc337-ef11-4d8d-ae73-5ae6d3acbb1a" />**

**<img width="640" height="74" alt="h5_Taskb_2" src="https://github.com/user-attachments/assets/539de6a5-c96f-4d3b-be67-dfee28add347" />**

**Tutorial Source:**
NeuralNine (2024). SSH Key Authentication on Linux Server: Easy Setup Tutorial.
YouTube. https://www.youtube.com/watch?v=6vTcH_kMrhU

## c) Password Manager

For this part of the assignment, I chose **KeePassXC**, an open‑source password manager that stores everything locally instead of relying on any cloud service.
It fits the requirements well: it's free, open source, and keeps all data inside an encrypted file on my own machine.

---

## Installation

I installed KeePassXC on my Debian/Ubuntu virtual machine using the package manager:

```bash
sudo apt update
sudo apt install keepassxc -y
```

Once the installation finished, I launched the program from the applications menu and it shows me the new window of KeePassXC as shown in the screenshot below:

**<img width="449" height="331" alt="h5_Taskc_1" src="https://github.com/user-attachments/assets/7e0bdc94-dbd9-4347-a333-29b717db64a5" />**

## Creating the Password Database
When KeePassXC opened, I created a new password database:
- Selected "New Database"
- Gave it a name
- Accepted the default encryption settings
- Set a strong master password
- Saved the resulting .kdbx file in my home directory with new folder named KeePass
This file is fully encrypted, and the master password is the only way to unlock it.

## Adding an Entry
- To demonstrate its use, I added a sample entry (can be seen in the following screenshot):
Title: Email
Username: myemail@gmail.com
Password: generated using KeePassXC's built‑in random password generator
URL: https://example.com

**<img width="640" height="230" alt="h5_Taskc_2" src="https://github.com/user-attachments/assets/1b002b86-03fc-4002-86c3-44bc1b723e11" />**

After saving the entry, it appeared in the main database view.

## Opening and Using the Database
- To verify that the database works as intended, I closed KeePassXC completely and opened it again.
- I selected "Open Database", navigated to my .kdbx file, and entered my master password.
- The database unlocked and displayed the entry I had created earlier.

To demonstrate password retrieval, I right‑clicked the entry and selected "Copy Password" visible in the below screenshot:

**<img width="393" height="84" alt="h5_Taskc_3" src="https://github.com/user-attachments/assets/89f94496-5b40-42bd-a065-a85c37807739" />**

KeePassXC copied the generated password to my clipboard, confirming that the manager can securely store and provide credentials when needed.

## Why a Password Manager Is Necessary
A password manager addresses several real‑world security problems:

### Password Reuse
Reusing the same password across multiple sites is extremely risky.
If one site is breached, attackers can try the same password elsewhere.
A manager makes it easy to use long, unique passwords for every account.

### Weak or Guessable Passwords
Human‑made passwords tend to be short or predictable.
A manager can generate strong, random passwords that resist brute‑force attacks.

### Phishing Protection
Many managers only autofill credentials when the website's URL matches exactly.
This helps prevent entering passwords into fake or look‑alike sites.

### Local Control (Cloudless Security)
KeePassXC stores everything in a local encrypted file, not in the cloud.
This reduces exposure to large‑scale cloud breaches and keeps the user in full control of their data.

## Summary
Using a password manager significantly improves security by:
- Reducing human error
- Strengthening password quality
- Preventing password reuse
- Protecting against phishing
- Keeping data fully local and encrypted

**References:**
GitHub. (2022). KeePassXC. Available at: https://github.com/keepassxreboot/keepassxc.
National Cyber Security Centre (2018). Password managers: How they help you secure passwords. www.ncsc.gov.uk. Available at: https://www.ncsc.gov.uk/collection/top-tips-for-staying-secure-online/password-managers.

---

## Voluntary Task: t) ROT13 Analysis

For this voluntary task, I explored how the ROT13 cipher behaves when applied multiple times.
ROT13 works by shifting each letter 13 positions forward in the alphabet. Because the alphabet has 26 letters, applying ROT13 twice returns the original message.

To test this, I wrote a short Python script using the `codecs` library.
When I encoded the word **HELLO** once, it became **URYYB**.
When I encoded **URYYB** again, it returned to **HELLO**.

This confirmed that **double ROT13 provides no additional security** - it is equivalent to not encrypting the message at all.

```python
import codecs

word = "HELLO"
once = codecs.encode(word, 'rot_13')
twice = codecs.encode(once, 'rot_13')

print("Original:", word)
print("Once:", once)
print("Twice:", twice)
```

The output showed:

**<img width="242" height="36" alt="h5_Taskt_1" src="https://github.com/user-attachments/assets/bca9dad0-9312-4db9-9ed8-ec61ca7b24d0" />**

This demonstrates that ROT13 is not a secure encryption method. It is mainly used for obfuscation, not protection.

And then just to play a little more with it, I changed the text of the word and noticed that Original replaced previous word text as our " new word text" but Once gives us a scrambled text, then Twice again restored our new word text, also shown below:

**<img width="275" height="40" alt="h5_Taskt_2" src="https://github.com/user-attachments/assets/082f0365-3912-47ea-a050-dbc364b3cea1" />**

So, it clarifies to me that basically ROT13 twice is same as original text.

### Conclusion
Double ROT13 does not increase security.
Because ROT13 is its own inverse, applying it twice simply returns the original text.
This makes it unsuitable for any real cryptographic purpose.

**Reference:**
GeeksforGeeks (2017). ROT13 cipher. https://www.geeksforgeeks.org/dsa/rot13-cipher/









