# mplayer3

mplayer3 is a lightweight compatibility layer that preserves the old-school
[MPlayer](http://www.mplayerhq.hu/) command-line interface while using
[mpv](https://mpv.io/) as its playback engine.

It lets you keep your old habits without giving up modern performance,
codec support, and hardware acceleration.

Released under GNU GPL.

---

## ✨ Features

- ✅ Classic `mplayer` CLI syntax (`-fs`, `-ss`, `-vo`, etc.)
- ✅ Automatic translation to `mpv` arguments
- ✅ Full support for native `mpv` arguments (`--vo=gpu`, etc.)
- ✅ Zero performance overhead
- ✅ Works with existing scripts and workflows
- ✅ Clean fallback: unknown arguments are passed through to `mpv`

---

## 🚀 Installation

### Requirements

- Python 3
- mpv installed and available in `PATH`

### Install

```bash
chmod +x mplayer3
sudo python3 install_mplayer3.py
```

This will:
- Install `mplayer3` to `/usr/local/bin`
- Create `~/.config/mpv/mpv.conf` (or safely append to an existing config)
- Create `~/.config/mpv/input.conf` (if not already present)

---

## 📖 Examples

```bash
mplayer3 video.mkv
mplayer3 -fs video.mkv
mplayer3 -ss 60 -endpos 120 video.mkv
mplayer3 --vo=gpu video.mkv
```

You can freely mix:
- **MPlayer-style arguments** (`-fs`, `-ss`)
- **MPV-style arguments** (`--hwdec=auto`)

---

## 🔁 Compatibility

mplayer3 translates common MPlayer arguments into mpv equivalents:

```
-fs        →  --fullscreen
-ss        →  --start
-endpos    →  --end
-volume    →  --volume
-sub       →  --sub-file
-playlist  →  --playlist
```

Unknown arguments are automatically passed through:

```
-someargument → --someargument
```

---

## 🧠 Philosophy

mplayer3 is:

- **Not a fork**
- **Not a reimplementation**
- **Not a replacement for mpv**

It is a **compatibility layer**:

> *mplayer in spirit, mpv in performance*

---

## ⚙️ Configuration

mplayer3 uses standard `mpv` configuration:

```
~/.config/mpv/mpv.conf
~/.config/mpv/input.conf
```

The installer adds a small compatibility block (OSD, volume behavior, etc.),
respecting existing user config strings by safely appending only missing
settings and avoiding duplicates.

---

## 💡 Basic Usage

```bash
mplayer3 -fs -ss 90 movie.mkv
```

> Starts playback fullscreen at 1:30 — just like classic mplayer.

---

## 👤 Author & Maintainer

- **Chris McGimpsey-Jones** (2026–Present)

## 🙏 Credits & Legacy

- **The MPlayer project** (2000–Present)
- **The mplayer2 project** (2010–2015)
- **The mpv project** (2012–Present)

---

## 🧩 Status

Version 1.2 (Stable)

---

## 📜 License

mplayer3 is released under the:

**GNU General Public License v2 or later (GPL-2.0-or-later)**  
https://gnu.org/licenses/gpl.html

This ensures compatibility with both:
- MPlayer (GPL v2+)
- mpv (GPL v2+)
