# h5 Alice and Bob

Here is report on the fifth assignment for the course - https://terokarvinen.com/cyber-security/

Instruction shown here https://terokarvinen.com/cyber-security/#agenda

---
### x) Read and summarize select chapters Schneier 2015: Applied Cryptography (with some bullet points)

**Applied Cryptography: Protocols, Algorithms and Source Code in C, 20th Anniversary Edition (2015), Bruce Schneier**

above is the source used for this part of the task.


**1. Bruce Schneier (2015) — Applied Cryptography, Chapter 1.1: Terminology**

- Messages & Core Operations: Plaintext (M) is the original readable message. Encryption (E) disguises plaintext into ciphertext (C). Decryption (D) reverses the process to recover original plaintext (D(E(M)) = M).
- Security Objectives: Cryptography provides confidentiality, along with three essential security goals:

  - Authentication: Verifying the true identity of the sender to prevent impersonation.
  - Integrity: Confirming the message was not modified or tampered with in transit.
  - Nonrepudiation: Preventing a sender from falsely denying they sent a message.

- Algorithms, Keys, and Kerckhoffs's Principle: Restricted algorithms rely on keeping the mathematical method secret, which fails in modern multi-user systems. Modern ciphers use a key (K). Under Kerckhoffs's principle, system security relies entirely on keeping the key secret, allowing the algorithm itself to be published and publicly scrutinized.

- Symmetric vs. Public-Key Algorithms:

* **Symmetric (Conventional):** Uses the same secret key for encryption and decryption (E<sub>k</sub>(M) = C, D<sub>K</sub>(C) = M).
Includes stream ciphers (operating bit-by-bit) and block ciphers (operating on fixed data blocks).
* **Public-Key (Asymmetric):** Uses a mathematically linked keypair. This public key encrypts  (K<sub>1).
* While decrypts is with the private key (K<sub>2)
* Decrypts D<sub>K2</sub>(E<sub>K1</sub>(M)) = M.
  
- Reversing this operation—encrypting with a private key and decrypting with a public key—forms digital signatures.

**2. Bruce Schneier (2015) — Applied Cryptography, Chapter 2.5: Public-Key Communications**

* **Mailbox Analogy & Key Distribution:** Public-key cryptography functions like a physical mailbox slot: anyone can drop a message in using the recipient's public key, but only the person holding the secret physical key can open the box to read it. This eliminates the key-distribution problem of symmetric ciphers.
* **Hybrid Cryptosystems:** Public-key ciphers are computationally slow and vulnerable to chosen-plaintext dictionary attacks on small message spaces. Practical protocols use hybrid encryption:

  1. Sender obtains recipient's public key.
  2. Sender creates a random symmetric session key (K), encrypts K with recipient's public key, and sends it.
  3. Recipient decrypts K with their private key.
  4. Both parties encrypt bulk payload data using the fast symmetric session key (K).

* **Merkle's Puzzles:** Ralph Merkle designed an early public-key concept where Bob sends Alice thousands of encrypted puzzle messages. Alice solves one puzzle using brute-force effort n. An eavesdropper Eve, not knowing which puzzle Alice selected, must brute-force all puzzles, requiring effort proportional to n^2.

**3. Tero Karvinen (2023) — PGP: Send Encrypted and Signed Message with gpg**

- **GnuPG Operations:** OpenPGP command-line tools (gpg) manage asymmetric keypairs. Public keys are exported in ASCII armor format (--export --armor) for easy sharing.
- **Trust & Verification:** Imported keys start with unknown trust. Users prevent Man-in-the-Middle (MitM) attacks by checking key fingerprints out-of-band and signing verified keys (gpg --sign-key) to establish full trust.
- **Integrated Encryption & Signing:** Senders encrypt using recipient public keys (`--encrypt --recipient`)  and sign using their own private keys (`--sign`). Recipients decrypt using their private key (gpg --decrypt), automatically verifying sender identity and message integrity.


### a) Pubkey today

In my daily student workflow at Haaga-Helia University of Applied Sciences, I use public-key cryptography whenever I log in to the Haaga-Helia Moodle learning portal (https://hhmoodle.haaga-helia.fi/login/index.php?loginredirect=1) over HTTPS using Transport Layer Security (TLS 1.3).

**Key Operations Across Protocol Steps**
- Certificate Authority (CA) Signing: The CA uses its private key to digitally sign Haaga-Helia's web server certificate. My browser verifies this certificate using the CA's public key pre-installed in the OS trust store.
- Server Authentication: During the TLS handshake, Haaga-Helia's server sends its certificate containing its public key. The server signs handshake data using its secret private key. My browser uses the server's public key to verify the signature, proving authentic server identity.
- Ephemeral Key Exchange (ECDHE): My browser and the server generate temporary Elliptic-Curve Diffie-Hellman private/public key pairs. Both exchange public keys and compute a shared secret without transmitting it over the network.
- Bulk Symmetric Encryption: Both parties derive symmetric session keys (such as AES-256-GCM) from the shared secret to encrypt all HTTPS traffic, ensuring confidentiality, integrity, and forward secrecy.

### b) Encrypt and decrypt a message.

one thing i want to note is that Public keys can be sent across an untrusted network, but still needs verification. Private keys on the other hand are kept confidential. A key should be deleted from everywhere it is used if it has been compromised due to leakage. Signing is authentic and integrity while Encryption gives confidentiality.

### PGP Encryption, Signing, and Verification with GNU Privacy Guard (`gpg`)- -**Cover d) Voluntary task**-

**Author:** Eddy  
**Environment:** Debian GNU/Linux (Oracle VirtualBox VM) 

---

## 1. Objective & Environment Setup

This lab demonstrates asymmetric cryptography—specifically encrypting, signing, decrypting, and verifying a message—between me, the receiver (**Eddy**) and a simulated sender (**Alice**) using GNU Privacy Guard (`gpg`) on Debian Linux.

First, the required tools (`gpg`, `micro` text editor, and `psmisc`) were installed:

```bash
eddy@debian:~$ sudo apt-get update
eddy@debian:~$ sudo apt-get install gpg micro psmisc
```

---

## 2. Step-by-Step Execution

### 2.1 Generating Receiver's Keypair (Eddy)
A primary Ed25519/Curve25519 keypair was generated for Eddy with an empty passphrase for lab purposes:

```bash
eddy@debian:~$ gpg --gen-key
```

Checking the generated fingerprint confirmed the keypair creation:

```text
pub   ed25519 2026-11-25 [SC] [expires: 2029-11-24]
      E6BEB377F087B3334475BE2C2575292C4C40C26F
uid           [ultimate] eddy DEMO KEY <eddy@example.com.invalid>
sub   cv25519 2026-11-25 [E] [expires: 2029-11-24]
```
<img width="1398" height="976" alt="WhatsApp Image 2026-11-25 at 16 17 39" src="https://github.com/user-attachments/assets/13299586-5d6f-4e63-bf46-c0d197a462d8" />

<img width="1352" height="965" alt="WhatsApp Image 2026-11-25 at 16 18 18" src="https://github.com/user-attachments/assets/b88750c1-7ef9-4d38-a591-3715fe3e0908" />


### 2.2 Exporting Eddy's Public Key
Eddy's public key was exported into an ASCII-armored text file (`--armor`) so it could be safely shared and copied:

```bash
eddy@debian:~$ gpg --export --armor --output eddy.pub
```

### 2.3 Creating a Simulated Sender (Alice)
Instead of provisioning a second virtual machine, a restricted directory (`~/alice/`) was created with `chmod og-rwx` so `gpg` would not warn about insecure permissions. Using `--homedir .` isolated Alice's keyring from Eddy's:

```bash
eddy@debian:~$ mkdir alice/
eddy@debian:~$ chmod og-rwx alice/
eddy@debian:~$ cd alice/
eddy@debian:~/alice$ gpg --homedir . --gen-key
```

Alice's generated keypair details:

```text
pub   ed25519 2026-11-25 [SC] [expires: 2029-11-24]
      1C60CD386214B79A5C9813D4510F14443DE04264
uid           [ultimate] Alice <alice@example.com.invalid>
sub   cv25519 2026-11-25 [E] [expires: 2029-11-24]
```

### 2.4 Exchanging & Verifying Public Keys (Establishing Trust)
In real-world usage, public keys can be transmitted over untrusted networks, provided both parties verify the 40-character fingerprints out-of-band (e.g., via voice call) before signing the keys.
<img width="1390" height="1016" alt="WhatsApp Image 2026-11-25 at 16 14 13" src="https://github.com/user-attachments/assets/c2c8ea49-3bf5-4ad9-8529-66beec00f844" />

Also below

<img width="1410" height="1006" alt="WhatsApp Image 2026-11-25 at 16 15 06" src="https://github.com/user-attachments/assets/ff43da0d-0105-44e3-8358-67ef81d55abe" />


**Alice imported and signed Eddy's public key:**
```bash
eddy@debian:~/alice$ cp -v ~/eddy.pub .
eddy@debian:~/alice$ gpg --homedir . --import eddy.pub
eddy@debian:~/alice$ gpg --homedir . --sign-key "E6BEB377F087B3334475BE2C2575292C4C40C26F"
```

**Eddy imported and signed Alice's public key:**
```bash
eddy@debian:~/alice$ gpg --homedir . --export --armor --output alice.pub
eddy@debian:~/alice$ cd
eddy@debian:~$ cp -v alice/alice.pub .
eddy@debian:~$ gpg --import alice.pub
eddy@debian:~$ gpg --sign-key "1C60CD386214B79A5C9813D4510F14443DE04264"
```

Running `gpg --fingerprint` in Eddy's home directory confirmed `[ full ]` trust on Alice's key:

```text
eddy@debian:~\$ gpg --fingerprint
/home/eddy/.gnupg/pubring.kbx
-----------------------------
pub   ed25519 2026-11-25 [SC] [expires: 2029-11-24]
      E6BE B377 F087 B333 4475  BE2C 2575 292C 4C40 C26F
uid           [ultimate] eddy DEMO KEY <eddy@example.com.invalid>
sub   cv25519 2026-11-25 [E] [expires: 2029-11-24]

pub   ed25519 2026-11-25 [SC] [expires: 2029-11-24]
      1C60 CD38 6214 B79A 5C98  13D4 510F 1444 3DE0 4264
uid           [  full  ] Alice <alice@example.com.invalid>
sub   cv25519 2026-11-25 [E] [expires: 2029-11-24]
```

### 2.5 Encrypting & Signing a Message (As Alice)
Alice created a plaintext file (`message.txt`) with `micro`, then encrypted it for Eddy (`--recipient`) and signed it with her own key (`--sign`):

```bash
eddy@debian:~\$ cd ~/alice/
eddy@debian:~/alice\$ micro message.txt
eddy@debian:~/alice\$ gpg --homedir . --encrypt --recipient eddy@example.com.invalid --sign --output encrypted.pgp --armor message.txt
eddy@debian:~/alice\$ head -5 encrypted.pgp
-----BEGIN PGP MESSAGE-----

hF4DQe8I+Rge2xISAQdAHevanVyur5Rs11YWFdgUsiL211fJYzdi4VXKJ3x9Scw
MUGE85m6iC7zsrMz0Fp75BYet5HkaaRNOK+cUuJZ1SQDIS25vuZ5rohXvZybhyOr
0sA6AC5G0glRcmw/A7roiHXeNihMzqyorrkGH0q7kpFy3pn00ukvgbidYc9t+Bew
```
*Notice that Because the file was encrypted using Eddy's public key, even Alice cannot decrypt `encrypted.pgp` once generated.*

### 2.6 Transferring, Decrypting & Verifying (As Eddy)
To simulate transmission over an untrusted network, `encrypted.pgp` was copied into Eddy's directory and decrypted:

```bash
eddy@debian:~/alice\$ cd
eddy@debian:~\$ cp -v alice/encrypted.pgp .
'alice/encrypted.pgp' -> './encrypted.pgp'
eddy@debian:~\$ gpg --decrypt encrypted.pgp
gpg: encrypted with cv25519 key, ID 41EF08F9181EDB12, created 2026-11-25
      "eddy DEMO KEY <eddy@example.com.invalid>"
Hi Eddy, this is my secret message protected by PGP! -- Alice
gpg: Signature made Wed 25 Nov 2026 15:56:27 EET
gpg:                using EDDSA key 1C60CD386214B79A5C9813D4510F14443DE04264
gpg: Good signature from "Alice <alice@example.com.invalid>" [full]
```

---

## 3. How Different Parties Use Different Keys

PGP combines two keypairs (four keys total) to provide **confidentiality** (only the intended recipient can read the message), **authenticity** (proof of sender identity), and **integrity** (detection of tampering):

| Stage of Operation | Active Party | Key Used | Purpose & Cryptographic Effect |
| :--- | :--- | :--- | :--- |
| **1. Key Verification** | Both (Out-of-Band) | Both **Public Keys** (Fingerprints) | Both users compare fingerprints over a trusted channel and sign each other's public keys to prevent Man-in-the-Middle (MitM) key substitution. |
| **2. Signing** | Sender (Alice) | **Alice's Secret Key** (`[SC]`) | Computes a cryptographic hash of the plaintext and signs it with Alice's private signing key. Proves Alice authored the message and that it has not been modified. |
| **3. Encryption** | Sender (Alice) | **Eddy's Public Key** (`[E]`) | Encrypts a random symmetric session key using Eddy's public encryption subkey (`cv25519`), locking the payload so only Eddy can open it. |
| **4. Decryption** | Receiver (Eddy) | **Eddy's Secret Key** (`[E]`) | Uses Eddy's private encryption subkey to unlock the symmetric session key and decrypt the ciphertext back into readable plaintext. |
| **5. Verification** | Receiver (Eddy) | **Alice's Public Key** (`[SC]`) | Verifies the attached signature against Alice's trusted public signing key, confirming `Good signature` and `[full]` trust. |

---

## 4. Security Evaluation of `gpg`

### Strengths
* **Modern, Battle-Tested Cryptography:** Modern `gpg` defaults to elliptic-curve cryptography (`ed25519` for signing and `cv25519` for encryption) paired with strong symmetric ciphers (such as AES-256), offering high security with compact key sizes.
* **Open-Source & Peer-Reviewed:** `gpg` is free, open-source software continuously audited by the global security community. It is trusted to sign Linux kernel releases and Debian package repositories.
* **Decentralized Trust Model:** Unlike TLS/HTTPS, which relies on centralized Certificate Authorities (CAs), PGP's Web of Trust allows two users to establish cryptographic trust directly without third-party intermediaries.

### Limitations & Operational Risks
* **Lack of Forward Secrecy (PFS):** Standard OpenPGP relies on static, long-lived encryption subkeys. If an attacker records encrypted traffic today and compromises Eddy's private key in the future, all previously captured messages can be decrypted retroactively.
* **Unencrypted Metadata:** While the message payload is encrypted, PGP headers still expose key IDs (`41EF08F9181EDB12`), timestamps, and message sizes to anyone intercepting the file in transit.
* **Endpoint & Passphrase Security:** Security depends entirely on protecting the private key directory (`~/.gnupg/`). In this lab, an empty passphrase was used for convenience; in production, an unencrypted private key stolen from a compromised machine allows complete impersonation and retroactive decryption.


## c) Password management

### Password Management with pass (The Standard Unix Password Manager)

*Environment:* Debian GNU/Linux (Oracle VirtualBox VM)  

---

### 1. Objective & Tool Overview

This report demonstrates the practical use of a password manager on Linux and analyzes the security risks faced by users who do not use one. For this exercise, I used **`pass`**, a lightweight command-line password manager that follows the Unix philosophy by storing each credential as an individual GPG-encrypted file inside `~/.password-store/`.

---

### 2. Step-by-Step Demonstration

### 2.1 Installation & Initialization
First, `pass` was installed via `apt-get` and initialized using my existing `ed25519` GPG key fingerprint (`E6BEB377F087B3334475BE2C2575292C4C40C26F`):

```bash
eddy@debian:~\$ sudo apt-get install pass
eddy@debian:~\$ pass init E6BEB377F087B3334475BE2C2575292C4C40C26F
mkdir: created directory '/home/eddy/.password-store/'
Password store initialized for E6BEB377F087B3334475BE2C2575292C4C40C26F
```

### 2.2 Generating and Inserting Credentials
Next, I generated a cryptographically random 20-character password for a simulated webmail service (`Email/example-webmail`) and manually inserted a multi-line entry containing both a password and username metadata (`Social/github-demo`):

```bash
eddy@debian:~\$ pass generate Email/example-webmail 20
mkdir: created directory '/home/eddy/.password-store/Email'
The generated password for Email/example-webmail is:
r@H!k'`MTQ,*eoA:{pA'

eddy@debian:~$ pass insert -m Social/github-demo
mkdir: created directory '/home/eddy/.password-store/Social'
Enter contents of Social/github-demo and press Ctrl+D when finished:

MyDemoPass2026!
username: eddy-demo
```
*(Note: The credentials shown above are strictly disposable lab test strings created for this demonstration.)*

### 2.3 Listing, Decrypting, and Verifying Encryption at Rest
Running `pass` displays the hierarchical directory structure of stored accounts, while `pass show` uses my GPG private key to decrypt a specific entry on demand:

```bash
eddy@debian:~$ pass
Password Store
├── Email
│   └── example-webmail
└── Social
    └── github-demo

eddy@debian:~$ pass show Email/example-webmail
r@H!k'`MTQ,*eoA:{pA'
```

Finally, inspecting the underlying file on disk with `file` confirms that it is stored as encrypted binary ciphertext (`data`) rather than readable plaintext:

```bash
eddy@debian:~\$ file ~/.password-store/Email/example-webmail.gpg
/home/eddy/.password-store/Email/example-webmail.gpg: data
```
<img width="1340" height="976" alt="WhatsApp Image 2026-11-25 at 17 25 11" src="https://github.com/user-attachments/assets/39234cf3-edd9-4318-8d3a-8a42ca2083f9" />

---

### 3. Attacks That Exploit Users Without Password Managers

Without a password manager, human memory limitations force users to choose short, predictable passwords and reuse the same credentials across multiple services. Attackers exploit these behaviors using several automated techniques:

| Attack Type | How It Works | How a Password Manager Prevents It |
| :--- | :--- | :--- |
| **Credential Stuffing** | Attackers take username/password pairs leaked from one breached website (via public data dumps) and use automated bots to test those exact combinations across thousands of other high-value services (email, banking, cloud). | Generates a **completely unique password for every website**. A breach on one platform cannot be used to compromise any other account. |
| **Password Spraying** | Instead of rapidly guessing many passwords against a single account (which triggers account lockouts), attackers test a handful of ultra-common passwords (e.g., `Winter2026!`, `Company123`) across thousands of user accounts. | Eliminates human-chosen patterns and predictable word/number substitutions by generating high-entropy random strings. |
| **Brute-Force & Dictionary Attacks** | Attackers run stolen password hashes through high-speed GPU cracking rigs using wordlists, leetspeak rules (`@` for `a`), and masks to recover weak or short passwords offline. | Creates long, complex passwords (e.g., 20+ random characters) whose massive keyspace makes offline cracking computationally infeasible. |
| **Phishing & Lookalike Domains** | Attackers trick users into typing credentials into spoofed websites (e.g., `g00gle.com` or `micros0ft-login.com`) that visually mimic legitimate login pages. | Browser-integrated password managers verify the **exact domain** before auto-filling and refuse to populate passwords on spoofed lookalike URLs. |
| **Plaintext Storage & Shoulder Surfing** | Users without managers often write passwords on sticky notes, store them in unencrypted text/spreadsheet files, or manually type them repeatedly in public spaces. | Encrypts all credentials at rest (using OpenPGP or AES-256) and copies passwords directly to the clipboard with automatic clearing (`pass -c`). |

**Threat Analysis (Risks of Manual Password Practices)**

- Credential Stuffing: Attackers use stolen username/password pairs from third-party breaches to log into other accounts. Password managers mitigate this by enforcing unique passwords for every site.
- Password Spraying: Attackers test common passwords (e.g., Spring2026!) across multiple accounts. Password managers eliminate predictable patterns by generating high-entropy random strings.
- Phishing & Domain Spoofing: Fake websites (e.g., typosquatting domains) trick users into typing passwords. Password managers match entries strictly against domain URLs; autofill fails on malicious sites, alerting the user.
- Keylogging: Endpoint malware records hardware keystrokes. Password managers use browser extensions and secure auto-fill IPC to bypass manual keyboard entry.
- Brute-Force & Dictionary Attacks: Automated scripts guess weak passwords. High-entropy generated passwords make dictionary and brute-force attacks computationally infeasible.

## References

- Karvinen, T. (2023). PGP - Send Encrypted and Signed Message - gpg. https://terokarvinen.com/2023/pgp-encrypt-sign-verify/
- Rescorla, E. (2018). The Transport Layer Security (TLS) Protocol Version 1.3 (RFC 8446). Internet Engineering Task Force (IETF). https://www.rfc-editor.org/info/rfc9846/ https://www.rfc-editor.org/rfc/rfc8446.html
- Schneier, B. (2015). Applied Cryptography: Protocols, Algorithms and Source Code in C (20th Anniversary ed.). John Wiley & Sons.
