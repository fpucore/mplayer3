
![MPlayer logo](https://www.qanonsec.com/images/i.php?/upload/2026/04/17/20260417091557-cd7a6235-xs.png)

# mplayer3

mplayer3 is forked from the [MPlayer](http://www.mplayerhq.hu/) and [mpv](https://mpv.io/) projects.

The project preserves the classic MPlayer command-line interface while running on a modern, properly 
engineered and maintained playback engine, keeping full hardware acceleration, codec support and 
MPlayer compatibility.

Released under GNU GPL.

---

## 🆕 What's New in v3.1.0

### FFMpeg+GStreamer Integration

In addition to built-in support for native FFMpeg (ffmpeg-next) framework, mplayer3 now includes 
user-friendly integration with the GStreamer framework via a pre-configured binary which is compiled 
on installation and then executed via the `mplayer3-gstreamer` prompt to play media using GStreamer 
decoding.
 
### Persistent Disk Cache

mplayer3 has introduced a dual-layer caching system that dramatically improves playback 
experience for local source files, especially large files over slow or network-mounted storage.

**How it works:**

When you play a local source file, mplayer3 does two things simultaneously:

1. **Disk cache** - The source file is silently copied to `~/.cache/mplayer3-disk-cache/` in 
   the background while playback begins immediately from the source. Once caching is complete, 
   playback seamlessly and invisibly switches to the cached copy. On repeat plays the cached copy
   is used instantly - no wait, no re-caching.

2. **RAM cache** - mplayer3 includes the in-memory (RAM) cache and is enabled on top of the
   disk cache, giving the decoder a fast buffer to work from and eliminating micro-stutters
   during playback.

Together, these two layers mean: **instant start, smooth seeking, stutter-free playback,
and fast repeat access** regardless of where the source file resides.

> Network streams and URLs bypass the disk cache and play directly through the engine.
> The RAM cache remains active for streams.

**Cache management:**

```bash
# Check cache location, number of entries and total size on disk
> mplayer3 -cache-status

# Delete all files from the disk cache
> mplayer3 -clear-cache
```

**Disabling the cache:**

```bash
# Play directly, bypassing the disk cache
> mplayer3 -no-disk-cache movie.mkv

# Disable the in-memory (RAM) cache
> mplayer3 -no-ram-cache movie.mkv

# Disable both caches, raw direct playback
> mplayer3 -no-disk-cache -no-ram-cache movie.mkv
```

**Double-dash forms are also accepted:**

```bash
> mplayer3 --cache-status
> mplayer3 --clear-cache

> mplayer3 --no-disk-cache movie.mkv
> mplayer3 --no-ram-cache movie.mkv
```

---

## ✨ Features

- ✅ Automatic arguments translation
- ✅ Classic `mplayer` CLI syntax (`-fs`, `-ss`, `-vo`, etc.)
- ✅ Full support for native `mpv3` arguments (`--vo=gpu`, etc.)
- ✅ Persistent disk cache for instant start and smooth repeat playback
- ✅ Automatic dual-layer caching (Disk + RAM)
- ✅ GStreamer integration
- ✅ OptimFROG playback
- ✅ Zero performance overhead
- ✅ X Server purity (Wayland disabled by default)
- ✅ Works with existing scripts and workflows

---

## 🚀 Installation

### Requirements

- `Python 3`
- `meson` and `ninja`
- A C compiler (e.g. `gcc` or `clang`) and classic build dependencies (ffmpeg 
  dev headers, libplacebo, libass, etc.). The installer does **not** validate 
  these — make sure they are in place before running it.

### Install

```bash
> gh repo clone https://www.github.com/fpucore/mplayer3

> goto mplayer3

> elevate $here/install_mplayer3.py
```

This will:

- Build the bundled `mplayer3` engine from source (`bin/`) using meson, as your
  invoking (non-root) user, and install it to `/usr/local/bin/mplayer3`
- Install `mplayer3` to `/usr/local/bin`
- Compile and install `mplayer3-ofr` and `mplayer3-gstreamer` binaries to `/usr/local/bin/`
- Create `~/.config/mplayer3/mplayer3.conf` (or safely append to an existing config)
- Create `~/.config/mplayer3/input.conf` (if not already present)

---

## 📖 Examples

### Playback (FFMpeg decoding)
```bash
> mplayer3 video.mkv
> mplayer3 -fs video.mkv
> mplayer3 -ss 60 -endpos 120 video.mkv
> mplayer3 --vo=gpu video.mkv
```

### Playback (GStreamer decoding)

```bash
> mplayer3-gstreamer video.mp4
> mplayer3-gstreamer audio.mp3
```

### Playback (OptimFROG codec)

```bash
> mplayer3-ofr audio.ofr
```

With mplayer3 you can freely mix:

- **MPlayer-style arguments** (`-fs`, `-ss`)
- **MPV-style arguments** (`--hwdec=auto`)

mplayer3 will perform an automatic translation of all arguments.

---

## 🔁 Compatibility

mplayer3 translates common arguments into workable equivalents:

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

It exists to give the classic MPlayer command-line interface a long-term home on top of a modern, maintained engine:

- The `mplayer3` CLI preserves the old `-fs`, `-ss`, `-vo` style arguments, translating them into workable equivalents — with full pass-through function.
- The engine is shipped in-tree so the whole stack builds and installs from a single source of truth.

---

## ⚙️ Configuration

mplayer3 uses a standard configuration:

```
~/.config/mplayer3/mplayer3.conf
~/.config/mplayer3/input.conf
```

The installer adds a small, tidy config block set, respecting existing user config 
strings by safely appending only missing settings and avoiding duplicates.

---

## 💡 Basic Usage

```bash
mplayer3 -fs -ss 90 movie.mkv
```

> Starts playback fullscreen at 1:30 — just like classic MPlayer.

---

## 👤 Author & Maintainer

- **Chris McGimpsey-Jones** (2026–Present)

## 🙏 Credits & Legacy

- **The mpv project** (2012–Present)
- **The mplayer2 project** (2010–2015)
- **The MPlayer project** (2000–Present)
- **The GStreamer Team** (2001-Present)
- **Florin Ghido** (OptimFROG codec) (1996-2022)

---

## 🧩 Status

Version 3.1.0 (Stable)

---

## 📜 License

mplayer3 is released under the:

**GNU General Public License v2 or later (GPL-2.0-or-later)**
https://gnu.org/licenses/gpl.html

This ensures compatibility with both:
- MPlayer (GPL v2+)
- mpv (GPL v2+)
