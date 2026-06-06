# video-editing-automation

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![CUDA](https://img.shields.io/badge/CUDA-GPU_accelerated-76B900?style=flat-square&logo=nvidia&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-363739?style=flat-square)
![Status](https://img.shields.io/badge/status-active-CCFF00?style=flat-square)
![Version](https://img.shields.io/badge/version-9.1-CCFF00?style=flat-square)

AI-powered video editor for long-form OBS footage. Drop in raw video, get back a tighter cut with subtitles and GPU-accelerated rendering.

## How it works

```text
raw .mp4
  |
  v
[Phase 1] Transcription  - faster-whisper large-v3, word-level timestamps, Malay + English
  |
  v
[Phase 2] Scoring        - transcript weight + audio energy + visual activity
  |
  v
[Phase 3] Topic grouping - gaps > 3.5s create new topics; long topics are split
  |
  v
[Phase 4] Selection      - top segments by quality mode
  |
  v
[Phase 5] Rendering      - ffmpeg concat + NVENC GPU encode
  |
  v
[Phase 6] Subtitles      - kinetic .ass + .srt, auto-burned
  |
  v
edited .mp4 + subtitles
```

## Genre presets

| Genre | Transcript | Audio | Visual |
|---|---:|---:|---:|
| Discord Call | 55% | 35% | 10% |
| Gaming | 30% | 30% | 40% |
| Vlog | 45% | 35% | 20% |

## Quality modes

| Mode | Cut target | Use case |
|---|---|---|
| Highlights | 62% kept | Short-form, reels |
| Balanced | 38% kept | Standard upload |
| Chill | 12% kept | Light trim only |

## Stack

- [`faster-whisper`](https://github.com/SYSTRAN/faster-whisper)
- `ffmpeg`
- `CUDA` with CPU fallback
- `tqdm`

## Requirements

```text
Python 3.10+
ffmpeg
NVIDIA GPU with CUDA (optional)
```

## Install

```bash
git clone https://github.com/arifaqyl/video-editing-automation
cd video-editing-automation
python -m venv venv
venv\Scripts\activate
pip install faster-whisper tqdm
```

## Usage

```bash
# Windows: double-click RUN.bat
# or run directly
python auto_cutter.py
```

Prompts:

1. Mode - Auto-cut or Manual trim
2. Select the `.mp4` path
3. Genre - Gaming / Discord / Vlog / Auto
4. Quality - Highlights / Balanced / Chill
5. Review in `review.html` and take the final `.mp4`

## Reaction word detection

The detector keeps common English and Malay reactions so highlights surface naturally.

```text
English: haha, bruh, bro, damn, yo, wait, clutch, gg, rip, omg
Malay:   gila, babi, pergh, walao, sial, bodoh, mampus, harap, eh
```

## Telegram completion notification

`notify.py` can send a Telegram message when a job finishes.

1. Copy `.env.example` to `.env` or set the variables in your shell.
2. Set:

```text
TG_BOT_TOKEN=your_bot_token
TG_CHAT_ID=your_chat_id
```

Every run is also appended to `processing_log.json` for local usage stats.

---

**[arifaqyl.me](https://arifaqyl.me)** · [github.com/arifaqyl](https://github.com/arifaqyl)
