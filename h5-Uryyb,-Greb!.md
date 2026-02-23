Uryyb, Greb! - Week 5
x.1) Schneier 2015 – Applied Cryptography: Chapter 1: Foundations
The shift from plaintext to ciphertext relies on algorithms combined with keys. Cryptography aims to achieve confidentiality, authentication, and integrity. Kerckhoffs’s principle states that security must depend on keeping the key secret rather than hiding the algorithm itself. Cryptographic methods fall into two main categories: symmetric systems and public‑key systems. At the lowest level, cryptography works with bits rather than characters.

Attack models include ciphertext‑only, known‑plaintext, chosen‑plaintext, and adaptive chosen‑plaintext attacks. Systems can be unconditionally secure or only computationally secure. We evaluate the difficulty of breaking a system by considering the amount of data needed, the processing effort required, and the storage demands.

Traditional ciphers can be defeated through frequency analysis and other modern cryptanalytic techniques. A simple XOR operation is considered trivial to compromise, even though it has been widely used commercially. The one‑time pad achieves perfect secrecy when the key is truly random and never reused. Well‑known modern algorithms include DES for symmetric encryption, RSA for public‑key encryption, and DSA for digital signatures. Open algorithms tend to be more reliable because they can be publicly examined and tested.

Although one‑time pads offer absolute security, they are impractical for most real‑world applications. Many “new” commercial ciphers are simply weak classical designs repackaged. Ultimately, cryptographic strength relies on making attacks so computationally expensive that they are not feasible. Over time, cryptography has moved from manipulating characters to performing mathematical operations on bits. Steganography takes a different approach by concealing the very presence of a message.

Reflection Question
If one‑time pads provide perfect secrecy but are too inconvenient for everyday use, what does that tell us about the trade‑off between ideal security and what people can realistically adopt?

Reference:  
CHAPTER 1: Foundations (2025). Applied Cryptography: Protocols, Algorithms and Source Code in C, 20th Anniversary Edition. O’Reilly Online Learning.
<https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/08_chap01.html#chap01-sec001>

x.2) PGP: Sending Encrypted and Signed Messages
PGP/GPG supports both message encryption and digital signatures. Public‑key cryptography makes it possible to communicate securely without sharing a secret key beforehand. Public keys are meant to be distributed freely, while private keys must remain confidential. Each person generates their own keypair using gpg --gen-key. Public keys can then be exported and shared with others.

To establish trust, fingerprints must be confirmed through a separate, reliable channel. When sending a message, the sender encrypts it with the recipient’s public key and signs it using their own private key. The recipient decrypts the message with their private key and checks the signature using the sender’s public key.

Key Commands Used
bash
gpg --gen-key
gpg --export --armor --output key.pub
gpg --import key.pub
gpg --encrypt --sign --recipient user@email.com message.txt
gpg --decrypt encrypted.pgp
Thoughts & Insights
The most challenging part is building trust. Even strong cryptography is useless if you end up trusting the wrong key.

Reference:  
Terokarvinen.com  (2023). PGP – Send Encrypted and Signed Message – gpg.  
<https://terokarvinen.com/2023/pgp-encrypt-sign-verify/>
