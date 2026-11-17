---
name: splicebay-studio
description: Use when cutting spoken retakes, trimming dead air, and balancing spoken audio locally or via an optional Splicebay Video Editor server.
argument-hint: "<video-path> [--client <slug>] [--transcript <json>] [--out <clean.mp4>]"
effort: medium
allowed-tools: Bash(gk *), Bash(./plugins/getknown-core/bin/gk *), Bash(node ./plugins/getknown-core/bin/gk *), Read, Edit, Write
---

# Video Rough-Cut & Spoken Audio Cleanup (`/splicebay-studio`)

Clean raw talking-head `.mp4`, `.webm`, or `.mov` takes locally on your Mac using `gk splicebay` (`ffmpeg` plus optional local `whisper-cli` word timestamps), or connect an optional **Splicebay Video Editor** server for multi-hook stem-cached batch renders and visual transcript timelines.

## Offline Local Engine vs. Optional Splicebay Video Editor

| Capability | Offline Local Mode (`$0.00`, Default) | Optional Splicebay Video Editor |
|---|---|---|
| **Transcription & Timing** | Local `whisper-cli` word/segment timestamps when a Whisper model (`~/.cache/whisper/ggml-base.en.bin` or `WHISPER_MODEL_PATH`) is present; emits a clear warning and runs acoustic silence cuts if no model is downloaded yet | Local deterministic ASR (`PROVIDER_MODE=local`) or Deepgram word timing (`PROVIDER_MODE=production`) |
| **Retake & Silence Cutting** | Physical dead-air and retake trimming via `ffmpeg` `trim`/`atrim` + `concat` with verified `ffprobe` before/after duration stats | Interactive transcript cleanup (`bulk_cleanup`, `swap_retake`) |
| **Audio Balancing** | `ffmpeg` highpass, speech compression, and loudness normalization | Multi-stem speech and ducked music mixes |
| **Beat Pacing & Hook Variants** | `<= 3.2 words/sec` beat budget check and 4-factor hook retention breakdown | `4 Hooks x up to 3 CTAs` stem-cached batch matrix |

## Step 1: Run Local Rough-Cut & Audio Cleanup

Pass your recorded video or audio take to `gk splicebay`:

```bash
./plugins/getknown-core/bin/gk splicebay clients/<client>/campaigns/<sprint>/assets/raw-take.mp4 \
  --client <client> \
  --out clients/<client>/campaigns/<sprint>/assets/clean-take.mp4
```

*(If `whisper-cli` is installed without a model file yet, run `./plugins/getknown-core/bin/gk setup-machine --download-whisper-model` once to save `ggml-base.en.bin` into `~/.cache/whisper` without scanning user home folders.)*

To validate a beat script or `capture-avatar.html` `.capture-transcript.json` file (`{ beats: [...] }` or array):
```bash
./plugins/getknown-core/bin/gk splicebay \
  --client <client> \
  --transcript clients/<client>/campaigns/<sprint>/drafts/reel-script.json
```

## Step 2: Optional Companion Splicebay Server

When a local (`http://127.0.0.1:3000`) or self-hosted Splicebay Video Editor instance is configured (`SPLICEBAY_URL` and optional `SPLICEBAY_API_KEY`, verified via `gk provider-health`), `gk splicebay` can call its HTTP and MCP tools (`list_projects`, `inspect_footage`, `propose_edit_plan`, `reelscut_cleanup_transcript`, `batch_hook_variations`, and `reelscut_render_and_wait`).
