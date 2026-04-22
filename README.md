# ⚙ The Aetheric Cipher Engine

**Version 1.0**  
*A browser-based Caesar Cipher tool with a steampunk aesthetic*

---

## Overview

The Aetheric Cipher Engine is a single-file, zero-dependency web application for encrypting and decrypting text messages using the Caesar Cipher algorithm. It operates entirely in the browser — no server, no data transmitted, no installation required.

The cipher shifts each character across the **printable ASCII range** (characters 32–126, giving 95 possible positions) by a user-chosen amount between −94 and +94. Applying the same shift in reverse perfectly recovers the original message.

---

## Features

- **Encrypt and Decrypt modes** — toggle between modes with a single click
- **Shift Key control** — type a value, use the ▲▼ stepper buttons, or click Random Shift
- **Random Shift** — generates a random key between −94 and +94
- **Brass gauge bar** — visual indicator of the shift position across the full range
- **Paste button** — reads directly from the clipboard (falls back to Ctrl+V prompt if access is blocked)
- **Copy button** — writes output to the clipboard (falls back to `execCommand` if the Clipboard API is unavailable)
- **Clear button** — wipes the input field
- **⇅ Use as Input** — transfers the output back into the input chamber and flips the mode, useful for chained operations
- **1,000 character limit** — enforced on typing, keyboard paste, and the Paste button
- **Live character counter** — turns red when 100 characters remain
- **Error banner** — appears when input is truncated due to the character limit
- **Help modal** — in-app operating instructions and changelog
- **Responsive layout** — fits on screen without scrolling; input and output panels sit side by side

---

## Usage

### Opening the app

Open `caesar-cipher.html` in any modern browser. No build step, no dependencies, no internet connection required (fonts load from Google Fonts if online; the app functions without them).

### Encrypting a message

1. Ensure **Encrypt** mode is selected (default).
2. Type or paste your message into the left panel (up to 1,000 characters).
3. Set your **Shift Key** — any integer from −94 to +94. Use the ▲▼ buttons, type directly into the dial, or click **⚄ Random Shift**.
4. Press **Engage the Engine** or hit **Enter**.
5. The encrypted ciphertext appears in the right panel. Click **⎘ Copy** to copy it.
6. Share the ciphertext *and* the shift key with the intended recipient — both are required for decryption.

### Decrypting a message

1. Switch to **Decrypt** mode.
2. Paste the ciphertext using the **⎘ Paste** button or **Ctrl+V**.
3. Enter the same Shift Key that was used to encrypt the message.
4. Press **Engage the Engine**.
5. The original message appears in the right panel.

---

## How the cipher works

The Caesar Cipher is a substitution cipher. Each printable ASCII character is shifted by a fixed number of positions within the printable range (32–126):

```
encrypted_code = ((original_code - 32 + shift) mod 95) + 32
```

Non-printable characters (e.g. newlines) are passed through unchanged.

The shift is normalised so that any integer input — including values outside ±94 or negative values — produces a valid, reversible result. A shift of 0 produces no change. A shift of +1 followed by a shift of −1 restores the original text.

**Example** with shift +3:

| Plaintext  | A  | B  | C  | …  | ~  |
|------------|----|----|----|----|-----|
| Ciphertext | D  | E  | F  | …  | !  |

---

## Character limit

Messages are capped at **1,000 characters**. The counter below the input field tracks usage and turns red when 100 characters remain. Any text pasted or typed beyond the limit is automatically truncated and an error banner is shown.

---

## Browser compatibility

Tested and working in all modern browsers:

| Browser         | Clipboard Paste | Clipboard Copy | Fallback |
|-----------------|-----------------|----------------|----------|
| Chrome / Edge   | ✓ Native        | ✓ Native       | —        |
| Firefox         | ✓ Native        | ✓ Native       | —        |
| Safari          | ✓ Native        | ✓ Native       | —        |
| Older browsers  | Ctrl+V prompt   | ✓ execCommand  | ✓        |

The Clipboard API requires either a secure context (HTTPS or localhost) or explicit browser permission. If access is blocked, the Paste button prompts the user to press Ctrl+V, and the Copy button falls back to `document.execCommand('copy')`.

---

## File structure

```
caesar-cipher.html   Single self-contained application file
README.md            This document
```

All HTML, CSS, and JavaScript are contained within `caesar-cipher.html`. There are no external scripts, no build tools, and no runtime dependencies beyond the Google Fonts stylesheet (which is optional).

---

## Technical notes

- **Cipher range:** ASCII 32 (`space`) through 126 (`~`) — 95 printable characters
- **Key range:** −94 to +94 (the full non-trivial shift range for 95 characters)
- **Shift normalisation:** `shift = ((shift % 95) + 95) % 95` — handles negative and out-of-range values
- **JS architecture:** Two namespaces — `App` (cipher logic and user actions) and `UI` (modal controls) — with all DOM references cached at startup for efficiency
- **No frameworks:** Vanilla HTML, CSS, and JavaScript only

---

## Changelog

### Version 1.0
- Initial release
- Full Caesar Cipher over printable ASCII range (±94 shifts)
- Steampunk aesthetic — brass/copper palette, riveted card, animated cog divider, gauge bar
- Two-column responsive layout — input and output side by side
- Encrypt and Decrypt modes with mode-aware button styles
- Shift Key dial with ▲▼ steppers and Random Shift
- Paste button (with Ctrl+V fallback) and Clear button on input
- Copy button with `execCommand` fallback on output
- ⇅ Use as Input swap control
- 1,000 character limit with live counter, red warning at 100 remaining, and error banner on overflow
- In-app Help modal with operating instructions and changelog

---

## Licence

This project is provided as-is for personal and educational use.
