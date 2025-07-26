### 🔐 What is SHA-1?

**SHA-1** stands for **Secure Hash Algorithm 1**.
It was developed by the **NSA** and published by **NIST** in **1995** as a **cryptographic hash function** used for data integrity.

---

## ✅ Key Features of SHA-1

| Feature                  | Description                                                                      |
| ------------------------ | -------------------------------------------------------------------------------- |
| **Hash Size**            | 160 bits (20 bytes)                                                              |
| **Input Type**           | Any-length binary data                                                           |
| **Output Format**        | Fixed-size hash (160-bit / 40 hex characters)                                    |
| **Speed**                | Fast and efficient (originally)                                                  |
| **Deterministic**        | Same input → always same output                                                  |
| **Pre-image Resistance** | Difficult to find input from a given hash (theoretically)                        |
| **Avalanche Effect**     | Small input change → drastic output change                                       |
| **One-Way Function**     | Cannot reverse from hash to original input                                       |
| **Collision Resistance** | Difficult to find two different inputs with the same hash (was true, now broken) |
| **Used In**              | Git, SSL certificates (historically), digital signatures (deprecated)            |

---

## 🧪 SHA-1 Hash Example

```bash
echo -n "hello" | sha1sum
```

**Output:**

```
aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d
```

---

## 🔐 Cryptographic Properties (Originally)

| Property                        | Purpose                                            |
| ------------------------------- | -------------------------------------------------- |
| **Pre-image resistance**        | Hard to find input from its hash                   |
| **Second pre-image resistance** | Hard to find a different input with the same hash  |
| **Collision resistance**        | Hard to find two inputs that produce the same hash |

---

## ❌ Weakness and Deprecation

SHA-1 is now **considered broken** and **not secure** due to:

| Problem                       | Details                                                                                                  |
| ----------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Collisions found**          | In 2017, Google and CWI Amsterdam found real SHA-1 collisions ([SHAttered attack](https://shattered.io)) |
| **Vulnerable to brute-force** | Computational power has made attacks feasible                                                            |
| **No longer trusted**         | Deprecated in SSL, TLS, digital signatures, and certificates                                             |

---

## 📉 SHA-1 vs SHA-2 vs SHA-3

| Feature         | SHA-1    | SHA-2 (SHA-256/512) | SHA-3 (Keccak)     |
| --------------- | -------- | ------------------- | ------------------ |
| Hash Size       | 160 bits | 256/512 bits        | Variable (224–512) |
| Collision Found | ✅ Yes    | ❌ No                | ❌ No               |
| Performance     | Fast     | Medium              | Slower             |
| Security        | Weak     | Strong              | Very Strong        |

---

## 🧰 Where SHA-1 Was (or Is) Used

| Usage                  | Status                                      |
| ---------------------- | ------------------------------------------- |
| **Git**                | Still used internally, migrating to SHA-256 |
| **Digital Signatures** | Deprecated                                  |
| **TLS Certificates**   | Deprecated since 2017                       |
| **Code Signing**       | Deprecated                                  |

---

## 📌 Summary

* SHA-1 is a **160-bit cryptographic hash function**
* Designed for data integrity and uniqueness
* **Now considered insecure** due to real-world collisions
* Replaced by **SHA-2** and **SHA-3** in modern applications

---

Next steps:

* A visual comparison between SHA-1 and SHA-256?
* Code examples in C++/Python for generating SHA-1?
* Explanation of how **SHA-1 works step-by-step internally** (bitwise operations, rounds)?


---

### Below are **simple examples in both Python and C++** to demonstrate:

* 🔐 **Hashing** (SHA-256)
* 🔐 **Encryption/Decryption** (AES)

---

## 🐍 Python Examples

### ✅ Hashing with SHA-256

```python
import hashlib

message = "hello world"
hash_object = hashlib.sha256(message.encode())
hex_dig = hash_object.hexdigest()

print("Original message:", message)
print("SHA-256 hash:     ", hex_dig)
```

---

### 🔐 AES Encryption/Decryption with `cryptography` library

> 🔸 First, install:

```bash
pip install cryptography
```

```python
from cryptography.fernet import Fernet

# Generate a key
key = Fernet.generate_key()
cipher = Fernet(key)

# Encrypt the message
message = "secret data".encode()
encrypted = cipher.encrypt(message)
print("Encrypted:", encrypted)

# Decrypt the message
decrypted = cipher.decrypt(encrypted)
print("Decrypted:", decrypted.decode())
```

---

## 💻 C++ Examples

### ✅ Hashing with SHA-256 using OpenSSL

> Compile with:

```bash
g++ sha256.cpp -lcrypto -o sha256
```

```cpp
#include <iostream>
#include <openssl/sha.h>

int main() {
    std::string input = "hello world";
    unsigned char hash[SHA256_DIGEST_LENGTH];

    SHA256((unsigned char*)input.c_str(), input.length(), hash);

    std::cout << "SHA-256: ";
    for (int i = 0; i < SHA256_DIGEST_LENGTH; ++i)
        printf("%02x", hash[i]);
    std::cout << std::endl;

    return 0;
}
```

---

### 🔐 AES Encryption/Decryption in C++ (OpenSSL Example)

> This is slightly advanced. AES requires padding, initialization vectors (IV), and a key.

Here is a simplified version (AES-128 ECB for demo only — **not recommended for production**):

```cpp
#include <openssl/aes.h>
#include <cstring>
#include <iostream>

int main() {
    AES_KEY enc_key, dec_key;
    unsigned char key[16] = "thisisa128bitkey"; // 16 bytes = 128-bit
    unsigned char text[16] = "secretmessage123"; // Must be 16 bytes
    unsigned char enc_out[16], dec_out[16];

    AES_set_encrypt_key(key, 128, &enc_key);
    AES_encrypt(text, enc_out, &enc_key);

    AES_set_decrypt_key(key, 128, &dec_key);
    AES_decrypt(enc_out, dec_out, &dec_key);

    std::cout << "Original : " << text << std::endl;
    std::cout << "Encrypted: ";
    for (int i = 0; i < 16; ++i) printf("%02x", enc_out[i]);
    std::cout << "\nDecrypted: " << dec_out << std::endl;

    return 0;
}
```

---

## 🔐 Summary

| Task       | Python Function    | C++ Equivalent (OpenSSL) |
| ---------- | ------------------ | ------------------------ |
| Hashing    | `hashlib.sha256()` | `SHA256()`               |
| Encryption | `Fernet.encrypt()` | `AES_encrypt()`          |
| Decryption | `Fernet.decrypt()` | `AES_decrypt()`          |

---

Would you like:

* A downloadable zip with working code?
* An example that includes **salted password hashing**?
* Example using **RSA encryption**?
