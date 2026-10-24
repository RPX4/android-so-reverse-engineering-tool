<div align="center">

# 🛡️ SO DAMPER

### The Legendary `.so` Reverse-Engineering & Analysis Toolkit

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![radare2](https://img.shields.io/badge/radare2-5.0%2B-red?style=for-the-badge)](https://rada.re)
[![Termux](https://img.shields.io/badge/Termux-Ready-green?style=for-the-badge&logo=termux)](https://termux.dev)
[![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20Linux-orange?style=for-the-badge&logo=linux)](https://kernel.org)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)
[![Bilingual](https://img.shields.io/badge/UI-Arabic%20%7C%20English-purple?style=for-the-badge)](README.md)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)]()

**Created with 💙 by [SHBILY](https://github.com/shbil7156-creator) & RP_X4@**

[العربية](#-الوصف-بالعربية) • [English](#-english-description) • [Screenshots](#-screenshots) • [Installation](#-installation)

---

</div>

## 📌 What is SO DAMPER?

**SO DAMPER** is a professional-grade **reverse-engineering toolkit** for `.so` (Shared Object) files on **Android and Linux**. It is designed for security researchers, malware analysts, CTF players, and reverse engineers who need to inspect native libraries quickly, elegantly, and with maximum coverage.

Unlike generic `strings` or `nm` tools, **SO DAMPER**:

- 🔥 **Combines two independent string-extraction engines** for maximum coverage
- 🧩 **Disassembles the entire binary** and **each ELF section separately**
- 🌐 **Presents results in a live bilingual interface** (Arabic/English)
- 📱 **Runs perfectly on Termux** (Android) — no PC needed

Whether you're analyzing an APK's native library, a CTF challenge, or a suspicious `.so` payload, **SO DAMPER** delivers a **clean, structured, ready-to-share report** in seconds.

---

## 🎯 Why Choose SO DAMPER?

| Feature | Why it matters |
|---------|----------------|
| 🔥 **Dual string engines** | `radare2` (izzj) + pure Python regex = **higher coverage** than any single tool |
| 🧩 **Per-section disassembly** | Understand `.text`, `.data`, `.rodata` **separately**, not as one blob |
| 🌐 **Bilingual (AR/EN)** | First RE tool with **full Arabic UI** including output file |
| 🎨 **Rich interactive UI** | Progress bars, colored tables, **live previews** of results |
| 📱 **Termux-native** | Built and tested for **on-device Android analysis** |
| 📝 **Structured report** | Unicode-framed output file, ready for reports / bug bounties |
| 🛡️ **Fail-safe** | One bad section never crashes the whole analysis |

---

## ✨ Feature Highlights

### 🔥 Dual String Extraction Engines

1. **Engine 1 — radare2 (`izzj`)**: full ELF-aware string scan with addresses and sizes.
2. **Engine 2 — Pure Python (regex)**: raw byte-level scan, catches strings radare2 may miss.

Both engines' results appear **separately** in the output file for easy comparison.

### 🧩 Full + Per-Section Disassembly

- **Full binary**: `pdf @@f` disassembles every detected function.
- **Per section**: reads ELF sections via `iSj` and disassembles each one independently.
- **Per section strings**: filters strings by vaddr range within each section.

### 🌐 Full Bilingual Support

Complete Arabic and English translations for:
- Console UI (prompts, previews, progress bar)
- **Output file content** (headers, section titles, summaries)

### 🎨 Interactive UI (rich library)

- ASCII banner with **SHBILY & RP_X4@** copyright.
- Progress bar showing **6 analysis stages**.
- Live `Table` and `Panel` previews of first 10 items per stage.
- Final statistics table + success panel.

---

## 📸 Screenshots

<div align="center">

| Banner & Language Select | Live Previews (rich) |
|:---:|:---:|
| ![Banner](screenshots/banner.jpg) | ![Strings Preview](screenshots/preview-strings.jpg) |

| ASM Preview | Sections Preview | Final Report |
|:---:|:---:|:---:|
| ![ASM Preview](screenshots/preview-asm.jpg) | ![Sections Preview](screenshots/preview-sections.jpg) | ![Final Report](screenshots/final-report.jpg) |

</div>

---

## ⚙️ Installation

### 📱 On Termux (Android)

```bash
pkg update && pkg upgrade -y
pkg install python radare2 -y
pip install r2pipe rich
```

🐧 On Linux (Debian / Ubuntu / Kali)

```bash
sudo apt update
sudo apt install python3 python3-pip radare2 -y
pip3 install r2pipe rich
```

📥 Clone the Repository

```bash
git clone https://github.com/shbil7156-creator/android-so-reverse-engineering-tool.git
cd android-so-reverse-engineering-tool
chmod +x SO_DAMPER.py
```

---

🚀 Usage

```bash
python3 SO_DAMPER.py
```

Workflow

1. Choose your language — 1 Arabic / 2 English.
2. Enter the .so file path — full path, or just the filename if it's in the same directory.
3. Watch live previews — first 10 strings, ASM lines, and sections.
4. Get your report — <filename>_analysis.txt in the same directory.

---

📄 Output File Structure

```
╔══════════════════════════════════════════╗
║      المحرك الأول: سلاسل radare2         ║  ← أول الملف
╚══════════════════════════════════════════╝
[0x00001000] (size= 14) Hello, world!
...

╔══════════════════════════════════════════╗
║      التفكيك الكامل للملف (ASM)          ║
╚══════════════════════════════════════════╝
;-- entry0:
0x00001000  push rbp
...

╔══════════════════════════════════════════╗
║   تحليل الأقسام (Sections) منفصلاً       ║
╚══════════════════════════════════════════╝
┌──── .text ────┐
│ تفكيك + سلاسل │
└───────────────┘
...

╔══════════════════════════════════════════╗
║   المحرك الثاني: Python الخالص           ║  ← آخر الملف
╚══════════════════════════════════════════╝
...

============================================================
إجمالي سلاسل radare2: 245
إجمالي سلاسل Python:  312
============================================================
حقوق النشر (c) SHBILY & RP_X4@
```

---

🧠 How It Works

```
┌──────────────────────────────────────────────────┐
│  1. r2pipe.open(so_path)       → open the file   │
│  2. r2.cmd("aaa")              → full analysis   │
│  3. r2.cmd("izzj")             → Engine 1 strings│
│  4. regex on raw bytes         → Engine 2 strings│
│  5. r2.cmd("pdf @@f")          → full disasm     │
│  6. r2.cmd("iSj")              → read sections   │
│  7. per section: pd + filter   → per-sec analysis│
│  8. write output file          → final report    │
└──────────────────────────────────────────────────┘
```

---

🛠️ Requirements

Requirement Version Role
Python 3.8+ Tool language
radare2 5.0+ Reverse-engineering engine
r2pipe latest Python ↔ radare2 bridge
rich 12.0+ Interactive UI

---

🎯 Use Cases

· 🔐 Malware analysis — inspect suspicious .so payloads inside APKs.
· 🏆 CTF challenges — quickly disassemble and extract strings from native libs.
· 🔍 Bug bounty — hunt for hardcoded secrets in Android libraries.
· 📚 Learning RE — see how sections map to actual code.

---

📜 License

Distributed under the MIT License. See LICENSE for details.

---

⚠️ Disclaimer

This tool is intended for educational and legitimate security research purposes only. Using it on files you do not have the right to analyze may violate local laws. The author is not responsible for any misuse.

---

<div align="center">

⭐ If this tool helped you, please star the repo! ⭐

Made with 💙 by SHBILY & RP_X4@

</div>
