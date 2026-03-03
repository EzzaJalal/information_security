# February2026! - Week 6

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

### 2.4 One‑Way Hash Functions

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

---

##### Reference
Schneier, B. and Diffie, W. (2015). *Applied Cryptography: Protocols, Algorithms, and Source Code in C.* Indianapolis (Ind.): Wiley.
