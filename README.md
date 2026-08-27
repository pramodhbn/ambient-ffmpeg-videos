# ambient-ffmpeg-macos
The audio system for Ambient for MacOS

Minimalist, LGPL v2.1+ pre-built FFmpeg binaries for macOS (`arm64` and `x64`), built specifically for local audio decoding in [Ambient](https://letsambient.com).

## Purpose & License Posture

* **LGPL v2.1+ Compliant**: Built strictly without GPL components (`--disable-gpl`, `--disable-nonfree`).
* **Lean Payload**: Stripped of video encoders and unrelated modules, reducing binary size to ~8–12 MB.
* **Dual Architecture**: Native builds for Apple Silicon (`darwin-arm64`) and Intel (`darwin-x64`).
* **Source & Build Transparency**: This repository contains the complete build scripts and GitHub Actions workflows used to generate the release binaries.
