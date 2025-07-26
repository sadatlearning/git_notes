### 🔐 How to Use `shasum` in Linux/macOS

The `shasum` command is used to **compute and verify SHA hash values** of files and strings. It supports multiple SHA algorithms (SHA-1, SHA-256, SHA-512, etc.) and is commonly used for verifying data integrity.

---

## 🧾 Basic Syntax

```bash
shasum [options] [file]
```

---

## ✅ Common Use Cases

### 1. 🔍 Compute SHA-1 Hash of a File

```bash
shasum myfile.txt
```

📌 Output:

```
5eb63bbbe01eeed093cb22bb8f5acdc3 myfile.txt
```

> Default algorithm is **SHA-1**

---

### 2. 🧠 Use SHA-256 Instead

```bash
shasum -a 256 myfile.txt
```

Output:

```
b94d27b9934d3e08a52e52d7da7dabfac484efe37a5380ee9088f7ace2efcde9 myfile.txt
```

| Algorithm | Option           |
| --------- | ---------------- |
| SHA-1     | `-a 1` (default) |
| SHA-256   | `-a 256`         |
| SHA-512   | `-a 512`         |

---

### 3. 🔐 Hash a String (via echo)

```bash
echo -n "hello world" | shasum -a 256
```

> `-n` prevents echo from adding a newline.

---

### 4. ✅ Verify a File's Integrity Using a Checksum File

First, generate a checksum file:

```bash
shasum -a 256 myfile.txt > checksum.sha256
```

Then verify:

```bash
shasum -a 256 -c checksum.sha256
```

✅ Output (if correct):

```
myfile.txt: OK
```

---

### 5. 📁 Hash All Files in a Directory

```bash
find . -type f -exec shasum -a 256 {} \;
```

---

## 🔐 Why Use `shasum`?

| Use Case                       | Why                                  |
| ------------------------------ | ------------------------------------ |
| Verify downloaded files        | Check against published SHA checksum |
| Ensure file integrity          | Detect tampering or corruption       |
| Store secure file fingerprints | For later verification               |

---

## 🧪 Example: Full Workflow

```bash
# 1. Generate checksum
shasum -a 256 bigfile.iso > bigfile.sha256

# 2. Later or on another system, verify it
shasum -a 256 -c bigfile.sha256
```

---

## 📝 Summary

| Task             | Command Example                    |
| ---------------- | ---------------------------------- |
| SHA-1 hash       | `shasum myfile.txt`                |
| SHA-256 hash     | `shasum -a 256 myfile.txt`         |
| SHA-512 hash     | `shasum -a 512 myfile.txt`         |
| Hash a string    | `echo -n "hello" \| shasum -a 256` |
| Verify hash file | `shasum -a 256 -c checksum.sha256` |

---

Would you like a shell script to:

* Automatically generate and verify SHA-256 checksums?
* Use `shasum` in CI/CD for file integrity checking?
