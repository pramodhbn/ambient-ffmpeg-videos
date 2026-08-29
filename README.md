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
  offer the GPL requires.
* **Lean payload**: `--disable-everything` plus only the video-assembly
  closure — h264/aac/png decode, libx264/aac encode, mov/concat/image2/lavfi
  in, mp4 out, scale/pad/fps filters.
* **Dual architecture**: Apple Silicon (`darwin-arm64`) and Intel
  (`darwin-x64`).
* **Sibling repos**: [ambient-ffmpeg-macos](https://github.com/pramodhbn/ambient-ffmpeg-macos)
  is the LGPL audio-decode build for Ambient (deliberately video-stripped);
  AmbientContent's Windows builds pin [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds)
  GPL releases by immutable tag + cross-verified SHA-256.
