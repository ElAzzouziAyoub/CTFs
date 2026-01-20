

# Complete Guide to Hashes, Passwords, and CTF Cracking

This guide explains in depth what hashes are, how they work, why they are irreversible, how they were used in the CTF you completed, and why password storage works the way it does. Reading this thoroughly will give you a **solid mental model** of hashing and password security.

---

## 1. What is a Hash?

A **hash** is a mathematical function that converts any input — like a password, a message, or a file — into a **fixed-length string of bits**. This output is called the **hash value** or **digest**.

Key properties of hashes:

- **Deterministic:** The same input always produces the same hash.  
- **Fixed length:** No matter how big or small the input, the hash has the same size (SHA-256 produces 256 bits).  
- **One-way:** You cannot reverse a hash to get the original input.  
- **Sensitive to changes:** Even changing a single character in the input produces a completely different hash.

### Example:

```text
Input: "qwert098"
SHA-256 hash: 916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745
