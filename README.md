
![MPlayer logo](https://www.qanonsec.com/images/i.php?/upload/2026/04/17/20260417091557-cd7a6235-xs.png)

# mplayer3

mplayer3 is a fork of the [MPlayer](http://www.mplayerhq.hu/) project, rebuilt
on top of a bundled fork of [mpv](https://mpv.io/) (called **mpv3**). It
preserves the classic MPlayer command-line interface while running on a modern,
maintained playback engine — full hardware acceleration, current codec support,
and no behavioural surprises.

One repo, one install, one philosophy: *mplayer in spirit, mpv in performance*.

Released under GNU GPL.

---

## ✨ Features

- ✅ Classic `mplayer` CLI syntax (`-fs`, `-ss`, `-vo`, etc.)
- ✅ Automatic translation to `mpv3` arguments
- ✅ Full support for native `mpv3` arguments (`--vo=gpu`, etc.)
- ✅ Zero performance overhead
- ✅ Works with existing scripts and workflows
- ✅ Clean fallback: unknown arguments are passed through to `mpv3`

---

## 🚀 Installation

### Requirements

- Python 3
- `meson` and `ninja`
- A C compiler (e.g. `gcc` or `clang`) and the standard mpv build dependencies
  (ffmpeg dev headers, libplacebo, libass, etc.). The installer does **not**
  validate these — make sure they are in place before running it.

### Install

```bash
chmod +x mplayer3
sudo python3 install_mplayer3.py
```

This will:
- Build the bundled `mpv3` engine from source (`mpv3/`) using meson, as your
  invoking (non-root) user, and install it to `/usr/local/bin/mpv3`
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

mplayer3 is a **fork** — of both MPlayer (in spirit and CLI) and mpv (in code and engine).

It exists to give the classic MPlayer command-line interface a long-term home on top of a modern, maintained playback engine:

- The `mplayer3` CLI wrapper preserves the old `-fs`, `-ss`, `-vo` style arguments, translating them into mpv equivalents — with full pass-through for native mpv options.
- The bundled **mpv3** engine is a fork of [mpv](https://mpv.io/), shipped in-tree so the whole stack builds and installs from a single source of truth.

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

Version 1.3 (Stable)

---

## 📜 License

mplayer3 is released under the:

**GNU General Public License v2 or later (GPL-2.0-or-later)**  
https://gnu.org/licenses/gpl.html

This ensures compatibility with both:
- MPlayer (GPL v2+)
- mpv (GPL v2+)
