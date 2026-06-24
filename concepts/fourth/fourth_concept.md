# BulletinOS — Features (v4)

## Core Concept
Wall-mounted smart bulletin board. Pi-driven, full-screen dashboard via Chromium kiosk, content postable remotely or by voice. Doubles as a homelab status display.

## Hardware
- **Compute:** Raspberry Pi 3B+ minimum, Pi 4 (2-4GB) preferred for headroom under kiosk + always-listening audio load
- **Display:** 16" HDMI panel, portrait orientation, 14" × 7.85" footprint
- **Mic:** ReSpeaker XVF3800 USB 4-Mic Array (enclosed version) — far-field pickup, onboard AEC/noise suppression/beamforming, no drivers
- **Enclosure:** Custom Fusion 360 case, clamshell split (front/back halves to fit print bed), tray-fit for display + Pi + mic, removable back panel for access

## Software / Pipeline
- **OS:** BulletinOS - custom barebones linux opperating system
- **Dashboard:** Custom web UI — homelab service status grid (ESPHome, Homepage, Immich, Jellyfin, n8n, Navidrome, Postgres, Prowlarr, qBittorrent, Radarr, SearXNG, Sonarr, etc.), live CPU/RAM/disk/RAM-used stats, CPU history graph
- **Posting API:** Flask REST API — post content to the board from anywhere on the network/internet
- **Voice pipeline:**
  - Always-on wake word detection on-device via Porcupine (low compute, runs fine on Pi)
  - On wake: audio captured via XVF3800, streamed to Optiplex for transcription (local Whisper)
  - Transcribed command parsed → routed to action (e.g. populate to-do task, post note, query status)
  - Result reflected back on dashboard
- **Networking:** Fits existing homelab stack — Tailscale for remote access, Cloudflare Tunnel / Nginx Proxy Manager if exposed beyond LAN

## Open / Next
- Confirm whether 16" panel is portrait-native or rotated landscape (display_rotate)
- Finalize Pi model (3B+ vs 4) based on observed load once kiosk + wake-word running together
- Case: confirm clamshell seam placement, vent layout, cable routing for HDMI/power/USB
- Define exact voice command set (initial scope: status query, add to-do, post note)