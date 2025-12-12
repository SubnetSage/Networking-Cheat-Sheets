# 🔐 Cryptography Cheat Sheet (Practical & Exam-Ready)

## 1️⃣ Core Goals of Cryptography

| Goal                | Meaning             |
| ------------------- | ------------------- |
| **Confidentiality** | Keep data secret    |
| **Integrity**       | Detect modification |
| **Authentication**  | Prove identity      |
| **Non-repudiation** | Can’t deny actions  |

---

## 2️⃣ Encryption Types

### 🔒 Symmetric Encryption

* Same key for encrypt/decrypt
* **Fast**, used for bulk data

| Algorithm | Notes                  |
| --------- | ---------------------- |
| AES       | Standard (128/192/256) |
| ChaCha20  | Fast, mobile-friendly  |
| 3DES      | Deprecated             |
| DES       | Broken                 |

📌 Used in: **TLS data, VPN tunnels, disk encryption**

---

### 🔑 Asymmetric Encryption

* Public / Private key pair
* **Slow**, used for key exchange

| Algorithm         | Notes                |
| ----------------- | -------------------- |
| RSA               | Legacy, still common |
| ECC (ECDSA, ECDH) | Modern, efficient    |
| Diffie-Hellman    | Key exchange only    |

📌 Used in: **TLS handshakes, certificates**

---

## 3️⃣ Hash Functions

* One-way functions
* Fixed-length output
* Used for integrity

| Hash              | Status |
| ----------------- | ------ |
| SHA-256 / SHA-384 | Secure |
| SHA-1             | Broken |
| MD5               | Broken |

📌 Hash ≠ encryption

---

## 4️⃣ Message Authentication

### HMAC

* Hash + secret key
* Prevents tampering

| Example     |
| ----------- |
| HMAC-SHA256 |

📌 Used in: **API auth, VPNs, TLS**

---

## 5️⃣ Digital Signatures

**Provides**

* Integrity
* Authentication
* Non-repudiation

**How it works**

1. Hash the message
2. Encrypt hash with **private key**
3. Verify with **public key**

📌 Used in: **Certificates, software signing, Git commits**

---

## 6️⃣ Key Exchange

| Method | Purpose                     |
| ------ | --------------------------- |
| RSA    | Legacy key exchange         |
| DH     | Secure shared secret        |
| ECDHE  | **Perfect Forward Secrecy** |

📌 **TLS uses ECDHE today**

---

## 7️⃣ Certificates & PKI

### X.509 Certificates Contain:

* Public key
* Identity (CN / SAN)
* Issuer
* Validity
* Signature

### PKI Components

| Component       | Role         |
| --------------- | ------------ |
| CA              | Issues certs |
| Intermediate CA | Trust chain  |
| Root CA         | Trust anchor |

---

## 8️⃣ TLS Crypto Stack (Modern)

```
ECDHE → RSA/ECDSA → AES-GCM / ChaCha20 → SHA-256
```

| Layer          | Function |
| -------------- | -------- |
| Key Exchange   | ECDHE    |
| Authentication | Certs    |
| Encryption     | AES-GCM  |
| Integrity      | AEAD     |

---

## 9️⃣ AEAD Ciphers (Modern Standard)

* Authenticated Encryption with Associated Data
* Encrypt + authenticate in one step

| Cipher            |
| ----------------- |
| AES-GCM           |
| ChaCha20-Poly1305 |

📌 Replaces “encrypt + MAC”

---

## 🔟 Key Sizes (Rule of Thumb)

| Algorithm | Secure Size |
| --------- | ----------- |
| AES       | 128+        |
| RSA       | 2048+       |
| ECC       | 256+        |
| SHA       | 256+        |

---

## 1️⃣1️⃣ Common Crypto Attacks

| Attack      | Mitigation           |
| ----------- | -------------------- |
| MITM        | Certificates, TLS    |
| Replay      | Nonces, timestamps   |
| Brute force | Key length           |
| Collision   | Strong hashes        |
| Downgrade   | Disable weak ciphers |

---

## 1️⃣2️⃣ Everyday Crypto Use Cases

| Use Case         | Crypto                   |
| ---------------- | ------------------------ |
| HTTPS            | TLS                      |
| VPN              | IPsec / WireGuard        |
| Wi-Fi            | WPA3                     |
| Disk Encryption  | AES                      |
| Password Storage | bcrypt / scrypt / Argon2 |
| Code Signing     | RSA / ECDSA              |

---

## 1️⃣3️⃣ Password Storage (🔥 Important)

❌ Never store plaintext
❌ Never use MD5/SHA alone

✅ Use:

* bcrypt
* scrypt
* Argon2

---

## 1️⃣4️⃣ Randomness

* Crypto depends on **strong entropy**
* Use **CSPRNGs**
* Bad randomness = broken crypto

---

## 🧠 Mental Models

* **Encrypt = confidentiality**
* **Hash = integrity**
* **Sign = trust**
* **TLS = crypto orchestration**

---

## 🔥 Crypto Myths (Avoid These)

❌ “Base64 is encryption”
❌ “Hashing can be reversed”
❌ “RSA encrypts all data”
❌ “Longer keys fix bad design”

---

