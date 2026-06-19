# Release Notes — v0.1.0 (Release Candidate)

**Date:** June 2026
**Status:** Private Beta / Release Candidate
**Platform:** Linux only

---

## Summary

Anion v0.1.0 is the first release candidate — a feature-complete Linux-only AI desktop operating layer. It includes an agentic assistant (ARIA), terminal intelligence, cross-device encrypted sync, and a comprehensive test harness.

## Implemented Features

### Core
- Python backend daemon architecture with systemd user services
- HTTP/SSE bridge on `127.0.0.1:9120`
- SQLite (WAL mode) memory and context engine
- Desktop window management (Sway, i3, X11)
- FUSE semantic filesystem

### ARIA Assistant
- ReAct-based agentic loop with 22 bounded tools
- Privacy redaction and risk tiers
- Approval gates for sensitive actions
- Token streaming over SSE
- Voice interaction (browser-based)
- Dynamic context-aware suggestions

### Terminal Intelligence
- SQLite-backed persistent history
- Deterministic risk preview for destructive commands
- Hybrid rule-based/LLM auto-recovery

### Cross-Device
- UDP LAN discovery and 6-digit PIN pairing
- NaCl Curve25519 E2E encrypted sync
- Conflict resolution modal
- Resume Context flow

### Desktop Shell
- Electron 33 + React 19 + Vite 8
- Three.js holographic Brain visualization
- ARIA widget dashboard with media player
- Ambient presence bar
- Dynamic continuity context

### Testing
- 742+ passing tests (pytest)
- Chaos, soak (24h), and DAST testing
- Automated Bandit SAST and pip-audit SCA

### Packaging
- Electron-Builder: AppImage + .deb
- systemd service installer

## Known Limitations

- Linux only — no Windows or macOS
- Voice relies on Chromium web-speech (native STT deferred)
- Docker deployment not recommended
- Manual setup required (no automated onboarding)

## Security Notes

- 0 committed secrets (24,700 files scanned)
- DAST clean (15 probes, no issues)
- 9 HIGH Bandit findings under audit (controlled subprocess calls)
- 65 dependency CVEs in dev environment (not in shipped artifacts)

## Next Release Goals

- Resolve dependency CVEs
- Complete subprocess security audit
- Implement native STT engine
- Add Flatpak packaging
- Launch public beta
