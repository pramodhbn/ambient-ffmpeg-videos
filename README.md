# ambient-ffmpeg-videos

The video assembly engine for AmbientContent on macOS.

Standalone, minimalist **GPL v2+** pre-built FFmpeg binaries for macOS
(`arm64` and `x64`), built specifically for LOCAL video assembly in
[AmbientContent](https://letsambient.com) — voiced clips + end cards become one
finished video, entirely on the user's machine.

## Purpose & license posture

* **GPL v2+** — these builds enable `--enable-gpl --enable-libx264`
  (libx264 is the universal *software* H.264 encoder, so assembly depends on no
  GPU and no OS media framework). `--disable-nonfree` and `--disable-version3`
  are kept. The binaries are invoked by AmbientContent as a **separate
  process**, never linked.
* **Corresponding source, by construction**: this repository contains the
  complete build scripts and GitHub Actions workflows, and every release names
  the exact FFmpeg and x264 sources it was built from. The repo IS the source
  offer the GPL requires — **and a release tag must sit on the commit whose
  workflow built it.** (Recorded, not hidden: `v7.1-gpl-video-2` shipped a
  wider closure than the workflow at its tag; the workflow was recovered from
  the shipped binaries' own configure lines on 11 Sep 2026 and committed —
  see the history note at the top of `.github/workflows/build.yml`.)
* **Lean payload**: `--disable-everything` plus only the closure
  AmbientContent's arg builders ask for — decode h264/hevc/aac/png/mjpeg/mp3/pcm,
  encode libx264/aac/png/mjpeg/pcm, in mov/concat/image2/mp3/wav/f32le/lavfi,
  out mp4/mov/image2/wav/f32le/null, filters scale/pad/fps/loudnorm/amix/xfade/
  acrossfade/sidechaincompress/overlay/trim/concat and the rest named in the
  workflow. Every entry is READ back from the built binary's listings by the
  Verify step, and the four working paths (lavfi input, the raw-f32le audio
  pipe, mp4 assembly, concat + xfade stitching) are DRIVEN and asserted.
* **Dual architecture**: Apple Silicon (`darwin-arm64`) and Intel
  (`darwin-x64`).
* **Sibling repos**: [ambient-ffmpeg-macos](https://github.com/pramodhbn/ambient-ffmpeg-macos)
  is the LGPL audio-decode build for Ambient (deliberately video-stripped);
  AmbientContent's Windows builds pin [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds)
  GPL releases by immutable tag + cross-verified SHA-256.

> **Meta** — v2 · Created: 27 Aug 2026 (initial) · Updated: Fri, 11 Sept, 2026, 10:27:07 IST *(v2: the source-offer sentence now says a tag must sit on the commit whose workflow built it, and the payload bullet names the real video-2 closure — recovered from the shipped binaries, MAC-1e step 1)*
