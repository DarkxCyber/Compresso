# Compresso: Client-Side File Compression and Encryption

**Compresso** is a browser-based utility packaged entirely as a **single HTML file**, enabling **Gzip compression** and optional **AES-GCM (256-bit) encryption** for multiple user files directly in your browser. Since all processing is done locally, **your files and passwords never leave your device**.


## Features
### Client-Side Processing:
All compression, encryption, and decryption tasks are executed entirely within your browser using the native Web Streams API and Web Crypto API. The application code is contained in a single file, ensuring maximum transparency and privacy.
### Gzip Compression:
Utilizes the highly efficient Gzip algorithm for standard compression.
### AES-GCM Encryption (Optional):
Securely encrypts compressed files using a 256-bit AES key derived from your password with PBKDF2.
### Multi-File Support"
Easily select and process multiple files in one batch.
### Simple Interface: 
Intuitive interface with file size and compression ratio feedback.
### Theme Toggle:
Supports both light and dark modes.


## How to Use
### **A. Compression and Optional Encryption**
1. **Select Files:**  
   Click "Click to select one or more files" and choose the files you want to compress.
2. **Set Password (Optional):**  
   If you want to encrypt the compressed file, enter a strong password in the input field. **If     you leave this field empty, only Gzip compression will be performed.**
3. **Compress:**  
   Click the **"Compress All Files"** button.
   • Output (No Password): The files will be downloaded as `[original-name].gz`.
   • Output (With Password): The files will be downloaded as `[original-name].gz.enc`.
### **B. Decompression and Decryption**
1. **Select Files:**  
   Select the compressed file(s) (`.gz` or `.gz.enc`).
2. **Decompress:**  
   Click the "Decompress All Files" button. 
3. **Password Prompt:**
   • If the file is encrypted (`.gz.enc`), the tool will either use the password you entered in       the main password field, or prompt you with a modal if the main field is empty.
   • If the file is not encrypted (`.gz`), decompression starts immediately. 
4. **Output:**
   The original files will be restored and downloaded (e.g., a compressed `file.txt.gz.enc` will    be restored to `file.txt`).


## Security and Technical Details
### **1. Zero-Trust, Zero-Upload Design**
**Compresso** is designed for maximum privacy. Since it is a single HTML file containing all logic, it can be run completely offline after the initial load. It does not use any server, tracking, or network requests for file processing.
### **2. Encryption Details**
• **Algorithm:** AES-256 in Galois/Counter Mode (GCM).
• **Key Derivation:** The encryption key is derived from your password using PBKDF2 (Password-     Based Key Derivation Function 2) with 100,000 iterations and SHA-256 hashing.
• **Metadata:** A 28-byte header is prepended to the encrypted data, consisting of a 16-byte       cryptographically random Salt (for key derivation) and a 12-byte cryptographically random        Initialization Vector (IV) (for AES-GCM)
### **3. File Format**
  When a file is encrypted, the output structure is:
  ` [ 16-byte Salt ] + [ 12-byte IV ] + [ Encrypted Gzip Data ]`
  The Gzip data is compressed first, and that entire compressed chunk is then encrypted.


## Development Stack
  • **Frontend:** Pure HTML/JavaScript
  • **Styling:** Tailwind CSS (loaded via CDN)
  **Core APIs:**
    • `**CompressionStream` / `DecompressionStream` (Gzip)
    • `crypto.subtle` (AES-GCM, PBKDF2)
    • `ReadableStream` (Stream processing)


## License
This project is open-source and available under the MIT License.
