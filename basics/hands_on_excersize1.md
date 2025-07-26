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
