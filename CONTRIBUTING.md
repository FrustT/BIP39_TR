# Contributing to BIP39_TR

Thank you for your interest in contributing to the Turkish BIP39 wordlist! This document explains how the wordlist is maintained and how you can propose changes.

---

## Wordlist Criteria

All words in `bip39_turkish.txt` must meet **all** of the following criteria:

| Criterion | Rule |
|---|---|
| Language | Turkish — recognisable to a native speaker |
| Character set | ASCII only (`a`–`z`). No ç, ğ, ı, ö, ş, ü |
| Minimum length | 4 characters |
| Maximum length | 8 characters |
| Unique prefix | First 4 characters must be unique across the entire list |
| No duplicates | Each word may appear only once |
| Common vocabulary | Avoid obscure, technical jargon, offensive, or easily confused words |
| Alphabetical order | The list must remain in ascending alphabetical (ASCII) order |

---

## How to Propose a Word Change

### Replacing a Word

If you believe a word should be replaced (e.g., it is offensive, ambiguous, or too obscure):

1. Open an [Issue](../../issues/new) describing:
   - The word you want to remove and why
   - A proposed replacement word (must satisfy all criteria above)
2. Verify that the replacement word:
   - Does not already exist in the list
   - Has a unique 4-letter prefix not shared by any current word
3. Submit a Pull Request with the change to `bip39_turkish.txt`

### Adding / Removing Words

The total word count **must remain exactly 2048**. Any PR that adds a word must also remove one, and vice versa.

---

## Validating Your Changes

Before submitting a PR, run the following checks locally:

```bash
# 1. Word count must be exactly 2048
wc -l bip39_turkish.txt

# 2. No duplicate words
sort bip39_turkish.txt | uniq -d

# 3. No duplicate 4-letter prefixes
awk '{print substr($0,1,4)}' bip39_turkish.txt | sort | uniq -d

# 4. No words shorter than 4 characters
awk 'length < 4' bip39_turkish.txt

# 5. No words longer than 8 characters
awk 'length > 8' bip39_turkish.txt

# 6. No non-ASCII characters
grep -P '[^\x00-\x7F]' bip39_turkish.txt

# 7. List is sorted alphabetically
sort -c bip39_turkish.txt
```

All of the above commands should produce **no output** (i.e., zero errors) for the wordlist to be valid.

---

## Pull Request Guidelines

- Keep PRs focused — one logical change per PR
- Include the validation output (all clear) in your PR description
- Explain *why* a word was added/removed/replaced
- Ensure the file ends with a newline

---

## Code of Conduct

Please be respectful and constructive in all interactions. This project follows the [Contributor Covenant](https://www.contributor-covenant.org/) code of conduct.
