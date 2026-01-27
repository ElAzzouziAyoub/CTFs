# zsteg — Steganography Tool (CTF-Oriented Overview)

## What is zsteg?
`zsteg` is a steganography analysis tool designed mainly for **PNG and BMP images**.  
It extracts hidden data embedded in **least significant bits (LSB)** of image pixels.

In CTFs, it’s commonly used when:
- The challenge mentions *images*, *colors*, *pixels*, or *hidden messages*
- `strings`, `exiftool`, and `binwalk` find nothing useful
- The file looks normal but smells suspicious

If you skip zsteg in image challenges, you’re either lazy or inexperienced.

---

## How Steganography Works (Quick Reality Check)
Images are made of pixels → pixels have color channels (R, G, B, A) → each channel is bytes → bytes have bits.

zsteg checks:
- Which **bit planes** (LSB, MSB)
- Which **channels** (R, G, B, A)
- Which **order** (xy, yx)
- Which **encoding** (ASCII, UTF-8, etc.)

Most CTF flags hide in **LSB**. Anything else is trying to be clever.

---

## Installation
```bash
gem install zsteg
```

Use zsteg --help for more info