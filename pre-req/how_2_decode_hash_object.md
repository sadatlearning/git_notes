
## 🔍 What Happens with `git cat-file -p <hash>`?

* It **decodes** and prints the human-readable content of the Git object.
* Git objects are stored in `.git/objects/` in compressed form. `cat-file` decompresses and shows them.

---

```bash
git cat-file -p <object-hash>
```

Is used to **inspect the content of a Git object**—such as a commit, tree, blob (file), or tag—by providing its **SHA-1 hash** (the “long hash keyword”).

---


## 📘 Examples

### 1. View a File’s Content (Blob)

```bash
git hash-object hello.txt
```

Output (e.g.):

```
b6fc4c620b67d95f953a5c1c1230aaab5db5a1b0
```

Now view its content:

```bash
git cat-file -p b6fc4c620b67d95f953a5c1c1230aaab5db5a1b0
```

Output:

```
Hello World!
```

---

### 2. View a Commit Object

```bash
git log --oneline
```

Sample:

```
7a25d0e First commit
```

Then:

```bash
git cat-file -p 7a25d0e
```

Output:

```
tree 1f7a7f0e...
author Kulkarni <you@example.com> 1699260000 +0530
committer Kulkarni <you@example.com> 1699260000 +0530

First commit
```

---

### 3. View a Tree Object

Get the tree hash from the commit above and:

```bash
git cat-file -p <tree-hash>
```

Output:

```
100644 blob b6fc4c620b67d95f953a5c1c1230aaab5db5a1b0    hello.txt
```

---

## 📚 Object Types You Can Explore

| Object Type | Description         |
| ----------- | ------------------- |
| `blob`      | File content        |
| `tree`      | Directory structure |
| `commit`    | Commit metadata     |
| `tag`       | Tag object info     |

You can find the type using:

```bash
git cat-file -t <hash>
```

---

## ✅ Summary

```bash
git cat-file -p <sha1-hash>
```

| You Get        | If Hash Is Of... |
| -------------- | ---------------- |
| File content   | Blob             |
| Directory info | Tree             |
| Commit info    | Commit           |
| Tag metadata   | Tag              |

Would you like a hands-on exercise to practice this with a sample Git repo and file?
