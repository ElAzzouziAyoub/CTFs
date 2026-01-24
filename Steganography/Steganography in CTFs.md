
Steganography is the practice of hiding data within other files. In CTFs, it’s commonly used to conceal flags inside images, audio files, or other media. Unlike encryption, steganography hides the **existence** of data rather than its content.

---

## Common File Types for Stego

| File Type | How Data Is Hidden |
|-----------|------------------|
| Images (BMP, PNG, JPG) | LSB (Least Significant Bit) of pixels, DCT coefficients (JPEG) |
| Audio (WAV, MP3) | LSB of audio samples, frequency coefficients |
| PDFs | Hidden objects, metadata, invisible layers |
| Other files | Unused headers, whitespace, binary padding |

---

## Typical Workflow in CTFs

### Hiding Data
1. **Encrypt (optional but recommended)**  
   - AES or other encryption with a password.
2. **Embed into carrier**  
   - LSB method for images/audio.
   - Tools: `steghide`, `zsteg`, `stegsolve`.
3. **Distribute or challenge**  
   - The file looks normal; the hidden data is invisible to casual inspection.

### Extracting Data
1. **Identify carrier**  
   - File type may give clues (e.g., `.png`, `.wav`).
2. **Analyze for stego**  
   - Tools: `steghide info/extract`, `zsteg`, `stegsolve`, `strings`.
3. **Decrypt payload if encrypted**  
   - Requires password or key if encryption was used.

---

## Key Concepts

### LSB (Least Significant Bit) Method
- Changes the last bit of each byte in an image or audio file.  
- Human perception is unaffected.  
- Example for a pixel:  
## Common CTF Tools

| Tool        | Purpose                                                   |
| ----------- | --------------------------------------------------------- |
| `steghide`  | Embed/extract data from images/audio (supports passwords) |
| `zsteg`     | Detect and extract hidden data in PNG/BMP images          |
| `stegsolve` | Analyze image layers and bit planes visually              |
| `binwalk`   | Inspect files for hidden payloads in binary blobs         |
| `strings`   | Quick check for readable text in binary files             |
