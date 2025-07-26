## Let’s do a **hands-on walkthrough** to understand how `git hash-object` fits into **Git internals** — particularly how Git stores files as **blob objects** inside the `.git/objects` directory.

---

## 🧪 Step-by-Step Git Internals with `git hash-object`

---

### ✅ Step 1: Create a New Git Repository

```bash
mkdir my-git-lab
cd my-git-lab
git init
```

> This creates a `.git/` directory where Git will store all its internal data.

---

### ✅ Step 2: Create a File

```bash
echo "Hello Git Internals" > test.txt
```

---

### ✅ Step 3: Compute SHA-1 Hash Without Storing It

```bash
git hash-object test.txt
```

🔸 Output:

```
<some 40-character hash>
e.g., 7f9d7b75a91dd8d6dfba55e55ed3cd357de3d3f7
```

This is the **SHA-1 hash** that Git would use internally to represent the file content.

---

### ✅ Step 4: Store It as a Git Blob Object

```bash
git hash-object -w test.txt
```

🔸 Again, you’ll get the same SHA-1 hash, but this time:

* Git stores the file’s contents as a **blob** inside `.git/objects/`

---

### ✅ Step 5: Inspect `.git/objects/`

```bash
ls .git/objects/
```

You’ll see a directory named with the **first 2 characters** of the hash (e.g., `7f`), and inside it:

```bash
ls .git/objects/7f/
```

You’ll find a file named with the **remaining 38 characters** of the hash (`9d7b75a91dd8d6dfba55e55ed3cd357de3d3f7`).

---

### ✅ Step 6: Read the Blob’s Content Using `git cat-file`

```bash
git cat-file -t <hash>
```

e.g.:

```bash
git cat-file -t 7f9d7b75a91dd8d6dfba55e55ed3cd357de3d3f7
```

🔹 Output: `blob`

To print its contents:

```bash
git cat-file -p 7f9d7b75a91dd8d6dfba55e55ed3cd357de3d3f7
```

🔹 Output:

```
Hello Git Internals
```

---

### ✅ Step 7: See the Blob’s Structure (Low-Level)

If you want to dig even deeper:

```bash
xxd .git/objects/7f/9d7b75a91dd8d6dfba55e55ed3cd357de3d3f7 | head
```

Git stores:

```
blob <length>\0<actual file content>
```

---

## 🧠 Recap: What You Just Did

| Step              | What Happened                            |
| ----------------- | ---------------------------------------- |
| `git hash-object` | Computed the SHA-1 of a file             |
| `-w` flag         | Stored it as a **blob** object in Git DB |
| `git cat-file`    | Verified the type and contents           |
| `.git/objects/`   | Explored Git's low-level content store   |

---

## 📦 Bonus: Create a Tree and Commit from the Blob (Manual Git Plumbing)

Would you like to go even deeper and manually create a **tree object** and then a **commit object** based on this blob (like Git does when you run `git commit`)?



---

Great! Here's a **step-by-step hands-on exercise** to help you understand how to use `git cat-file -p <hash>` to inspect internal Git objects like **blobs, trees, and commits**.

---

## 🧪 Goal:

Explore the Git internal database and retrieve original file content, directory structure, and commit metadata using SHA-1 hashes.

---

## 📁 Step-by-Step Git Object Inspection Exercise

---

### ✅ Step 1: Create a New Git Repo

```bash
mkdir git-obj-demo && cd git-obj-demo
git init
```

---

### ✅ Step 2: Create a File and Commit

```bash
echo "Hello Git Internals" > message.txt
git add message.txt
git commit -m "Initial commit"
```

---

### ✅ Step 3: Get the SHA-1 of the File (Blob)

```bash
git hash-object message.txt
```

You will get output like:

```
e964df013a2dba098f2dfdccac89d1e1d98bc6a2
```

Now view the content of the **blob**:

```bash
git cat-file -p e964df013a2dba098f2dfdccac89d1e1d98bc6a2
```

📦 **You’ll see:**

```
Hello Git Internals
```

---

### ✅ Step 4: Get the Latest Commit Hash

```bash
git log --oneline
```

Sample output:

```
5b48f96 (HEAD -> master) Initial commit
```

Now inspect the **commit object**:

```bash
git cat-file -p 5b48f96
```

📦 You’ll see:

```
tree 0d1e7bb8...       # This is the tree hash
author ...
committer ...

Initial commit
```

---

### ✅ Step 5: Inspect the Tree (Directory Structure)

Take the `tree` hash shown above and run:

```bash
git cat-file -p 0d1e7bb8
```

You’ll see:

```
100644 blob e964df013a2dba098f2dfdccac89d1e1d98bc6a2	message.txt
```

🔍 This tells you:

* `message.txt` is stored as a **blob**.
* Its hash is `e964df01...` (same as above).
* It has permissions `100644` (normal file).

---

## 🔁 Summary Flow

```text
Commit --> Tree --> Blob (file content)

git cat-file -p <commit>  --> shows tree + metadata
git cat-file -p <tree>    --> shows file name + blob hash
git cat-file -p <blob>    --> shows file content
```

---

## 🧰 Bonus Commands

| Purpose              | Command                  |
| -------------------- | ------------------------ |
| Get object type      | `git cat-file -t <hash>` |
| Pretty print content | `git cat-file -p <hash>` |
| SHA of file only     | `git hash-object <file>` |
| Commit SHA           | `git rev-parse HEAD`     |

