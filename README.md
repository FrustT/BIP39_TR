# BIP39_TR — Turkish BIP39 Wordlist

A Turkish mnemonic word list for [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) seed phrase generation.

---

## What is BIP39?

[BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) (Bitcoin Improvement Proposal 39) defines a standard for generating human-readable mnemonic phrases that encode a cryptographic seed. These mnemonics are widely used in cryptocurrency wallets (Bitcoin, Ethereum, and others) to allow users to back up and restore their wallets using a sequence of words.

A BIP39 mnemonic typically consists of 12, 15, 18, 21, or 24 words chosen from a standardised wordlist of exactly **2048 words**.

---

## About This Wordlist

This repository provides a **Turkish (TR) BIP39 wordlist** — `bip39_turkish.txt` — containing **2048 unique Turkish words** that meet all BIP39 requirements.

> **Note:** This is an unofficial, community-maintained wordlist and is not endorsed by the BIP39 authors or any official standards body.

### Key Properties

| Property | Value |
|---|---|
| Total words | 2048 |
| Min word length | 4 characters |
| Max word length | 8 characters |
| Character set | ASCII-only (a–z) |
| Unique 4-letter prefixes | ✅ All 2048 words have a unique first-4-letter prefix |
| Duplicate words | None |
| Turkish special characters | None (ç, ğ, ı, ö, ş, ü avoided for maximum compatibility) |

### Word Length Distribution

| Length | Count |
|---|---|
| 4 letters | 287 |
| 5 letters | 583 |
| 6 letters | 569 |
| 7 letters | 359 |
| 8 letters | 250 |

---

## Word Selection Criteria

Words in this list were selected according to the following criteria:

1. **Turkish origin** — All words are common Turkish words recognisable to native speakers.
2. **ASCII-only** — No Turkish-specific diacritics (ç, ğ, ı, ö, ş, ü) are used, ensuring the wordlist works on any system and keyboard layout without encoding issues.
3. **Length: 4–8 characters** — Short enough to type quickly, long enough to be distinctive.
4. **Unique 4-letter prefix** — The first four characters of every word are unique across the entire list, meaning users (and software) only need to type the first four characters to unambiguously identify a word.
5. **No duplicates** — Every word appears exactly once.
6. **Common vocabulary** — Obscure, offensive, or confusable words are avoided.

---

## File Format

`bip39_turkish.txt` contains one word per line, with no numbering or extra formatting — ready to be consumed directly by BIP39-compatible libraries.

```
abadi
abajur
abana
...
zuhur
```

> **Note:** The file contains exactly 2048 lines / words.

---

## Usage

### Python (with `mnemonic` library)

```python
from mnemonic import Mnemonic

# Load the custom Turkish wordlist
with open("bip39_turkish.txt", "r", encoding="utf-8") as f:
    wordlist = [line.strip() for line in f if line.strip()]

mnemo = Mnemonic.__new__(Mnemonic)
mnemo.wordlist = wordlist

# Generate a 12-word mnemonic
entropy = mnemo.generate(strength=128)
print(entropy)
```

### JavaScript / Node.js (with `bip39` library)

```javascript
const bip39 = require('bip39');
const fs = require('fs');

const wordlist = fs.readFileSync('bip39_turkish.txt', 'utf8')
  .split('\n')
  .filter(Boolean);

// Generate a mnemonic using the Turkish wordlist
const mnemonic = bip39.generateMnemonic(128, undefined, wordlist);
console.log(mnemonic);
```

---

## Validation

You can quickly validate the wordlist with the following shell commands:

```bash
# Count words (should be 2048)
wc -l bip39_turkish.txt

# Check for duplicate words
sort bip39_turkish.txt | uniq -d

# Check for duplicate 4-letter prefixes
awk '{print substr($0,1,4)}' bip39_turkish.txt | sort | uniq -d

# Check for words shorter than 4 characters
awk 'length < 4' bip39_turkish.txt

# Check for words longer than 8 characters
awk 'length > 8' bip39_turkish.txt
```

---

## Word Source

The Turkish words in this list were sourced from the TDK (Türk Dil Kurumu) dictionary data made available by the [TDKDictionaryCrawler](https://github.com/ncarkaci/TDKDictionaryCrawler) project. Words were then filtered and curated to meet the BIP39 technical requirements listed above.

---

## Comparison with Other BIP39 Wordlists

The [official BIP39 repository](https://github.com/trezor/python-mnemonic) includes wordlists for English, Japanese, Korean, Spanish, Chinese (Simplified & Traditional), French, Italian, Czech, and Portuguese. This repository provides a community-maintained Turkish wordlist following the same technical conventions, but is not part of that official collection.

---

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting changes.

---

## License

This project is licensed under the [MIT License](LICENSE).

Copyright © 2026 Burak Erinç