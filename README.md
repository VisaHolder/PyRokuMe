<div align="center">

# PyRokuMe

**A compact, keyboard-driven Roku remote for Windows — no browser, no Electron, just Python.**

[![Version](https://img.shields.io/badge/version-1.0.1-00ffe5?style=flat-square)](https://github.com/reaprrr/PyRokuMe/releases)
[![Python](https://img.shields.io/badge/python-3.8%2B-6c2bd9?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![Platform](https://img.shields.io/badge/platform-Windows-6868a0?style=flat-square&logo=windows)](https://github.com/reaprrr/PyRokuMe)
[![License](https://img.shields.io/badge/license-MIT-39ff7f?style=flat-square)](LICENSE)

<br/>

<img src="preview.svg" alt="PyRokuMe app preview" width="220"/>

</div>

---

## What is it?

PyRokuMe is a single-file Python remote control for Roku devices. It auto-discovers Rokus on your network, presents a full button layout in a compact resizable window, and gets out of your way. It uses Roku's built-in [ECP (External Control Protocol)](https://developer.roku.com/docs/developer-program/debugging/external-control-api.md) over HTTP — no Roku account, no cloud, no tracking.

---

## Features

- **Auto-discovery** — finds Roku devices via SSDP multicast and a parallel IP range scan; manual IP entry as fallback
- **Full remote layout** — Back, Home, Mute, Power, D-pad, OK, Vol±, Ch±, Rewind, Play/Pause, FF
- **Keyboard shortcuts** — full keyboard mapping, fully remappable via ⚙ Settings → Edit Key Bindings
- **App launcher** — browse and launch installed channels directly from the remote
- **Input switcher** — quickly switch HDMI inputs from a popup
- **Send text** — type and send text character-by-character to your Roku via ECP
- **Wake on LAN** — send a magic packet to wake your Roku/TV from sleep; fires automatically on Power press if a MAC is saved
- **Now playing** — live status bar showing what's currently playing
- **System tray** — minimises to tray; right-click for quick actions
- **Multi-device** — save and quick-switch between multiple Rokus
- **6 colour themes** — Dark, Terminal, Ice, Sunset, Midnight, Light — switch live with no restart
- **Opacity control** — slide the window transparency from 20% to 100%
- **Always on Top** — optional setting to keep the remote above other windows
- **Auto-reconnect** — silently re-establishes connection if the Roku goes to sleep and wakes
- **Portable or Standard** — choose on first launch: config next to the exe, or in `%APPDATA%`
- **Resize from corner** — drag the bottom-right grip to resize; drag the title bar to move

---

## Requirements

- Windows 10/11
- Python 3.8+ (not needed if using the compiled `.exe`)
- `requests` (auto-installed on first launch if missing)

All other dependencies (`tkinter`, `socket`, `threading`, `ctypes`) are part of the Python standard library.

---

## Installation

### Compiled EXE (recommended)

Download `PyRokuMe.exe` from [Releases](https://github.com/reaprrr/PyRokuMe/releases) and run it. No Python required.

On first launch you'll be asked whether to run in **Portable** mode (config saved next to the exe) or **Standard** mode (config saved to `%APPDATA%\PyRokuMe\PyRokuMe.json`).

### From source

```bash
git clone https://github.com/reaprrr/PyRokuMe.git
cd PyRokuMe
pip install requests
python PyRokuMe.pyw
```

### Build EXE yourself

```bash
pip install pyinstaller
pyinstaller --onefile --windowed --icon=app.ico --name PyRokuMe PyRokuMe.pyw
```

---

## Keyboard Shortcuts

| Key(s) | Action |
|---|---|
| `W` / `↑` | Up |
| `S` / `↓` | Down |
| `A` / `←` | Left |
| `D` / `→` | Right |
| `Enter` / `Space` / `O` | OK / Select |
| `Backspace` / `B` | Back |
| `Escape` / `H` | Home |
| `I` | Info |
| `,` / `R` | Rewind |
| `.` / `F` | Fast Forward |
| `/` / `P` | Play / Pause |
| `[` / `-` | Volume Down |
| `]` / `+` | Volume Up |
| `\` / `M` | Mute |

All bindings are remappable from **⚙ Settings → Edit Key Bindings**.

---

## Themes

| Name | Description |
|---|---|
| **Dark** *(default)* | Deep navy background, cyan accent |
| **Terminal** | GitHub-dark palette, blue accent |
| **Ice** | Cold deep-blue tones, sky accent |
| **Sunset** | Warm dark reds, orange accent |
| **Midnight** | Deep indigo, purple/magenta accent |
| **Light** | White background for bright environments |

Switch themes from the 🎨 button in the title bar. Changes apply instantly.

---

## How it works

PyRokuMe communicates with your Roku using its built-in **External Control Protocol (ECP)** — a simple HTTP API that every Roku device exposes on port `8060`. No pairing, no authentication.

Discovery uses two methods simultaneously:
1. **SSDP** — sends a multicast probe to `239.255.255.250:1900` and listens for Roku responses
2. **TCP scan** — probes `192.168.2.1` through `192.168.2.99` in parallel threads, checking if port `8060` is open

---

## File structure

```
PyRokuMe/
├── PyRokuMe.pyw      # entire application — single file
├── PyRokuMe.json     # auto-created: saved devices, theme, position, keybinds
├── app.ico           # application icon
├── requirements.txt  # pip dependencies (requests only)
├── CHANGELOG.md      # version history
├── LICENSE
└── README.md
```

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for the full version history.

---

## License

MIT — see [LICENSE](LICENSE) for details.

---

<div align="center">
<sub>Built with Python + tkinter · Styled after <a href="https://github.com/reaprrr/PyDisplay">PyDisplay</a></sub>
</div>
