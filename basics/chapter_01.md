## 🧱 1. What Is a **Git Blob**?

A **blob** (binary large object) in Git stores the **contents of a file**, but **not its filename or location**.

### 🔧 How it works:

* When you `git add message.txt`, Git:

  * Compresses file contents
  * Computes a SHA-1 hash from the content (including a header)
  * Stores it in `.git/objects/` using the first 2 characters as a directory

### 📦 Blob Example

```bash
echo "Hello Git" > demo.txt
git hash-object demo.txt
```

Output:

```
d3f11e05d58b7722cb6e8c8b85c5f19b2373d420
```

Inspect it:

```bash
git cat-file -t d3f11e05d58b7722cb6e8c8b85c5f19b2373d420  # -> blob
git cat-file -p d3f11e05d58b7722cb6e8c8b85c5f19b2373d420  # -> Hello Git
```

So, a **blob is pure content**. No filename, no directory structure.

---

## 🌳 2. Git Objects: The Full Picture

Git has **4 object types**, all stored in `.git/objects/`:

| Type     | Description                            |
| -------- | -------------------------------------- |
| `blob`   | File content only                      |
| `tree`   | Directory structure (filenames, blobs) |
| `commit` | A snapshot of the tree + metadata      |
| `tag`    | An annotated tag for a commit          |

### 🗂 Object Relationships

```text
Commit
  └── Tree
       ├── Blob (file1)
       └── Tree (subdir/)
             └── Blob (file2)
```

### 🔎 Example Flow

1. Create and commit a file:

   ```bash
   echo "Hi" > a.txt
   git add .
   git commit -m "Add a.txt"
   ```

2. View commit:

   ```bash
   git rev-parse HEAD       # -> commit hash
   git cat-file -p <commit-hash>
   ```

3. Find tree and inspect it:

   ```bash
   git cat-file -p <tree-hash>
   ```

4. Find blob and inspect content:

   ```bash
   git cat-file -p <blob-hash>
   ```

Each object references the next using a **SHA-1 hash**. That brings us to the last part...

---

## 🔐 3. How Git SHA-1 Works

Git computes a SHA-1 hash based on:

```text
<type> <size>\0<actual content>
```

For example:

```bash
echo "Hello Git" > file.txt
git hash-object file.txt
```

Git prepends a header:

```
blob 10\0Hello Git
```

Then computes:

```text
SHA-1("blob 10\0Hello Git") => d3f11e...
```

This guarantees:

* Identical content always gives same hash.
* Any content change yields a new hash.
* Git doesn’t need timestamps—hash identifies content.

You can verify it manually using:

```bash
printf "blob 10\0Hello Git" | sha1sum
```

---

## 🔁 Recap

| Component | Stores                                  | Identified By       |
| --------- | --------------------------------------- | ------------------- |
| Blob      | File content                            | SHA-1               |
| Tree      | File names, permissions, blob/tree refs | SHA-1               |
| Commit    | Tree ref + metadata                     | SHA-1               |
| SHA-1     | Secure 160-bit hash of the object       | Always 40 hex chars |

---

## 📘 Next Steps

Would you like me to:

* Show how Git stores these objects physically?
* Build a simple in-memory Git blob/tree simulator in Python/C++?
* Give a visual flowchart of Git object relationships?

Let me know what you'd like next!
