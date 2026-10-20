# ShortForge Studio 🎬

A Streamlit app to turn long videos **you own or have the right to edit** into vertical 9:16 YouTube Shorts.

## Features

- Paste a single public YouTube video link (where downloading is permitted), **or upload an MP4/MOV/MKV/WEBM**.
- Generate 1–100 short clips, up to **180 seconds each** (source length / overlaps / processing limits apply).
- **Smart Highlights** uses subtitles, speech density, hook keywords and audio levels (no paid service).
- **AI Highlights (optional)** uses your own OpenAI API key to semantically rank transcribed candidates; billed separately.
- Evenly spaced and manual-timestamp alternatives.
- Edit each clip's source timestamps and headline in a table before rendering.
- 540p / 720p / 1080p vertical outputs; crop-to-fill or blurred-background framing.
- Burn original subtitles when available; optionally overlay the selected headline.
- Preview and download individual MP4 files or one ZIP, plus CSV with selected timestamps.

> **Important:** "Smart" is a heuristic ranking, not a promise to identify viral clips. AI semantic ranking sees transcript excerpts, not the video itself. For best results, review and edit the suggestions.

## Deploy to Streamlit Community Cloud

1. Create a public or private GitHub repository named `shortforge-studio`.
2. Upload the **contents of this folder** to the repository root, preserving `.streamlit/config.toml`.
3. Open https://share.streamlit.io and choose **Create app** / **Deploy an app**.
4. Select your GitHub repository, branch `main`, and entrypoint `streamlit_app.py`.
5. Choose Python **3.11 or 3.12** if available, then deploy. Dependencies come from `requirements.txt` and system packages from `packages.txt`.
6. Paste a YouTube link or upload your own video, confirm your rights, and click **Load video** → **Find highlights** → **Generate all MP4 Shorts**.

**If YouTube download fails:** YouTube may block automated downloads in hosted environments, require login or PO Tokens, or restrict formats. This application does not bypass those protections. Use an authorized local video file upload instead.

**Cloud limitations:** Streamlit Community Cloud has limited CPU, RAM, temporary storage, upload and download memory. For long (1+ hour) source videos or dozens of 1080p exports, run locally or use a more powerful paid server. The app has no background worker; a disconnect/restart may stop a render and temporary files may disappear.

## Run locally (recommended for large projects)

Install Python 3.11 or 3.12 and **FFmpeg** (`ffmpeg` and `ffprobe` must be in your PATH). Then:

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
# source .venv/bin/activate
python -m pip install -r requirements.txt
streamlit run streamlit_app.py
```

A browser window opens. YouTube availability still depends on its access restrictions.

## Captions and optional AI

- The app attempts to retrieve available English, Azerbaijani, Russian or Turkish captions from the linked YouTube video.
- For uploaded videos, provide your own `.srt` / `.vtt` if you want text-based ranking and burnt-in captions. Without captions, free Smart Highlights uses audio-energy peaks.
- Optionally select **AI Highlights (optional)** and enter your *personal* API key directly into the app. This sends shortlist transcript excerpts to OpenAI, may incur API charges, and is not needed for normal usage.
- Never commit API keys to GitHub or put them in `.py` files.

## How to create more clips

The user can request up to 100. Non-overlapping clips are limited by the video's duration. **Smart Highlights** returns as many distinct candidates as fit; **Evenly spaced** can produce more clips by letting them overlap. Output count and quality also depend on available compute and storage.

## YouTube compliance

Use recordings you own or are authorized to edit and publish. Reuploading minimally altered third-party footage may trigger copyright claims or fail monetization checks under YouTube's reused-content policies, even with a technically successful conversion. Shorts can be vertical/square and up to 3 minutes, subject to YouTube's current rules.

This tool **does not auto-publish** to YouTube. Download the MP4s and upload them via YouTube Studio.
