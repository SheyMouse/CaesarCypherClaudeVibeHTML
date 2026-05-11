# Caesar Cipher

A browser-based Caesar Cipher tool. No installation, no server, no data transmitted — open the HTML file and go.

---

## What is the Caesar Cipher?

The Caesar Cipher is one of the oldest and simplest encryption techniques. It works by shifting every character in a message a fixed number of positions along a known sequence. To decrypt, the recipient applies the same shift in reverse. For example, with a shift of +3, the letter **A** becomes **D**, **B** becomes **E**, and so on.

This implementation operates over the full printable ASCII range — characters 32 through 126 (space to tilde), giving 95 possible positions. Any character outside that range (such as newlines) passes through unchanged.

```
encrypted_code = ((original_code − 32 + shift) mod 95) + 32
```

The Caesar Cipher is not intended for serious security use, but it is a clean demonstration of substitution ciphers and is perfectly serviceable for casual encoding.

---

## Version History

| Version | Theme | Notable Changes |
|---------|-------|-----------------|
| **1.0** | Steampunk (brass & copper) | Initial release. Single shift key (±94). Manual encrypt/decrypt. Paste, Copy, Swap, Clear. 1,000 character limit. |
| **2.0** | Retro C64 (blue screen, VT323 font) | Redesigned as a mobile-first layout. Live encryption as you type. Shift key repositioned above the output field for one-thumb use. |
| **3.0** | Retro C64 | Dual shift keys (±94 each), both silently embedded in the output — the recipient needs no separate key exchange. Live output. Download (.txt) and Share buttons added. Auto key detection on decrypt. |
| **4.0** | Retro C64 | Version bump. All internal version references updated. |

---

## Using Version 4.0

Open `caesar-cipher-04_webapp.html` in any modern browser.

### Encrypting a message

1. Make sure **Encrypt** is selected in the mode strip at the top.
2. Type or paste your message into the input field (up to 1,000 characters). Encryption happens live as you type.
3. Set **Shift Key 1** and **Shift Key 2** — any integer from −94 to +94 each. Use the ▲▼ steppers, type directly into the field, or hit the random button.
4. The encrypted ciphertext appears immediately in the output area. Both shift keys are silently embedded in the first two characters of the output, so the recipient does not need to know the keys separately.
5. Use **[ DOWNLOAD ]** to save the ciphertext as a `.txt` file, or **[ SHARE ]** to send it via your system share sheet (falls back to clipboard copy if unavailable).

### Decrypting a message

1. Switch to **Decrypt** mode.
2. Paste the ciphertext into the input field. The app automatically extracts the embedded shift keys and displays them as **AUTO** — you do not need to enter them manually.
3. The decrypted message appears live in the output area.
4. Use **[ DOWNLOAD ]** or **[ SHARE ]** to export the result.

### Other controls

- **PASTE** — reads from the clipboard (falls back to a Ctrl+V prompt if clipboard access is blocked).
- **CLEAR** — wipes the input field.
- **⇅ / SWAP** — moves the output back into the input and flips the mode; useful for chaining operations.
- **?** — opens the in-app help modal with instructions and the full changelog.
- The character counter below the input turns red when 100 characters remain. Input is hard-capped at 1,000 characters.

### Browser compatibility

The app works in all modern browsers. The Clipboard API and Web Share API require either a secure context (HTTPS or localhost) or explicit browser permission; both fall back gracefully if unavailable.

---

## File Structure

```
caesar-cipher-01.html      Version 1.0 — steampunk theme
caesar-cipher-02.html      Version 2.0 — C64 theme, mobile-first
caesar-cipher-03_webapp.html   Version 3.0 — dual keys, embedded key transport
caesar-cipher-04_webapp.html   Version 4.0 — current release
README.md                  This document
```

Each file is fully self-contained: all HTML, CSS, and JavaScript in a single file, no build step, no dependencies beyond an optional Google Fonts stylesheet.

---

## Licence

Provided as-is for personal and educational use.
