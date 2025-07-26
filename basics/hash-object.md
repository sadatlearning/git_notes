## What is git hash-object command do

- The `git hash-object` command is used to **compute and store the SHA-1 hash** of a file's content **as a Git object**, or just to **see the hash**, depending on how you use it.

---

## 🔍 Syntax

```bash
git hash-object [options] <file>
```

---

## 🧠 What Does It Do?

| Use Case                         | Description                                                              |
| -------------------------------- | ------------------------------------------------------------------------ |
| **Compute hash only**            | Shows the SHA-1 hash Git would use for the file                          |
| **Store object in Git database** | Actually stores the content as a "blob" in Git's internal `.git/objects` |

---

## 📦 Git Internals: Why It's Important

Git stores files as **blobs** (binary large objects) identified by the **SHA-1 hash** of their contents.
This command simulates or performs that action.

---

## 🧪 Example: View SHA-1 Hash (No Storage)

```bash
git hash-object myfile.txt
```

* Outputs a 40-character SHA-1 hash (like `5eb63bbbe01eeed093cb22bb8f5acdc3`)
* This is the hash Git would use internally if you added this file to the repo

---

## 💾 Example: Hash and Store in Git Object Database

```bash
git hash-object -w myfile.txt
```

* The `-w` option **writes** the object into Git's `.git/objects` directory
* It creates a **blob object**
* This is how Git tracks file content behind the scenes

---

## 🧰 Common Use Cases

| Task                                 | Command                                   |
| ------------------------------------ | ----------------------------------------- |
| Just get file’s Git-style SHA-1 hash | `git hash-object file.txt`                |
| Store file as blob in Git DB         | `git hash-object -w file.txt`             |
| Use in plumbing/low-level scripting  | Part of Git plumbing (low-level commands) |

---

## 🔎 What’s Inside the Hash?

Git doesn’t hash the raw file contents. It does this instead:

```plaintext
blob <size>\0<file contents>
```

Then it computes the SHA-1 of that whole blob. This ensures consistent hashes for identical content.

---

## 📌 Summary

| Feature                | `git hash-object`          |
| ---------------------- | -------------------------- |
| Purpose                | Hashes a file as Git would |
| Output                 | 40-char SHA-1 hash         |
| Stores file in Git DB? | Only with `-w`             |
| Git object type        | **blob**                   |
| Usage Level            | Low-level plumbing command |

---

Would you like a hands-on walkthrough to explore Git internals (like inspecting the blob object created with this command)?
