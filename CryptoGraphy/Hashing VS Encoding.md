

## Hashing

### What a Hash Is
A **hash** is the output of a **hash function**.
It takes input data of any size and produces a **fixed-length value**.

Example:
- Input: `"hello"`
- Output (SHA-256):  
  `2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824`

That output is the **hash**.

---

### Core Properties of Hashing
A cryptographic hash function has these properties:

1. **One-way**
   - You cannot reverse a hash to recover the original data.

2. **Deterministic**
   - Same input → same hash.

3. **Fixed output length**
   - Input size does not affect output size.

4. **Avalanche effect**
   - Small input change → completely different hash.

---

### Purpose of Hashing
Hashing is used for **verification**, not data recovery.

Common uses:
- Password storage
- File integrity checks
- Digital fingerprints (Git, malware, blockchains)
- Fast comparison of large data

---

### Hashing Is NOT Encryption
- No keys
- Not reversible
- Designed to destroy information

If something uses a key, it is **not hashing**.

---

## Encoding

### What Encoding Is
**Encoding** converts data into another format so it can be:
- Stored
- Transmitted
- Displayed

Encoding is **fully reversible**.

Example (Base64):
- `"hello"` → `aGVsbG8=` → `"hello"`

---

### Properties of Encoding
- Reversible
- No security purpose
- No secrecy
- No keys

Encoding does **not** protect data.

---
### Purpose of Encoding
Encoding exists for **compatibility**, not security.

Common uses:
- Sending binary data over text-based protocols
- Character representation (ASCII, UTF-8)
- Data transport and formatting

---

## Hashing vs Encoding (Direct Comparison)

| Feature | Hashing | Encoding |
|------|-------|--------|
| Reversible | ❌ No | ✅ Yes |
| Security-related | ✅ Yes | ❌ No |
| Fixed output length | ✅ Yes | ❌ No |
| Uses a key | ❌ No | ❌ No |
| Purpose | Verification | Representation |

---
## Common Mistake
Thinking a hash is “encoded text” is **wrong**.

- Encoding changes how data looks
- Hashing destroys data to create a fingerprint

---

## Important Clarification: RSA
RSA is **NOT hashing**.

- RSA is asymmetric encryption and digital signatures
- RSA is reversible using keys
- Hashing is irreversible and keyless

RSA **uses hashes** in digital signatures, but it is not a hash itself.

---

## Mental Model (Do Not Forget)
- **Encoding**: “How do I represent this data?”
- **Hashing**: “Does this data match?”
- **Encryption (RSA)**: “Who can read this?”

---

## One-Sentence Rule
**Encoding hides nothing. Hashing hides everything — on purpose.**
