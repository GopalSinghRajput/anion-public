# Changelog

All notable changes to Anion will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [0.1.0] — Release Candidate — 2026-06-18

### Added
- **ARIA Agentic Assistant** — ReAct-based voice and text assistant with 22 bounded tools, privacy redaction, risk tiers, and approval gates
- **Terminal Intelligence** — Smart CLI wrapper with SQLite-backed history, risk preview for destructive commands, and hybrid rule-based/LLM auto-recovery
- **Context & Memory Engine** — Continuous indexing of active windows, terminal operations, and filesystem events into local SQLite (WAL mode)
- **Cross-Device Sync** — Custom UDP LAN discovery with 6-digit PIN pairing and NaCl Curve25519 E2E encrypted channels
- **Live Neural Brain** — Three.js-powered holographic visualization responding to real-time system load
- **Feature Activation Engine** — Context-aware UI nudges with dynamic policy refinement based on user acceptance
- **Desktop Window Management** — Live Sway/i3/X11 monitoring via `wmctrl`, `xdotool`, `swaymsg`, `i3-msg`
- **ARIA Widget Dashboard** — Primary landing page with interactive widget grid and cross-session media player
- **Dynamic Continuity Context** — Real-time unfinished work and triage suggestions in the Continuations interface
- **Ambient Presence Bar** — Lightweight top-bar showing live system state
- **Pinned Files Context** — Attach local files to the LLM context for targeted queries
- **Conflict Resolution Modal** — 3-way merge UI for cross-device state collisions
- **Plugin Sandbox-Lite** — RLIMIT (Memory/CPU/FD) constraints for plugin execution
- **Unified Semantic Ranking** — 7-factor ranking engine for search results (semantic similarity, keywords, recency, workspace fit)
- **Token Streaming** — Real-time text chunking over SSE
- **Pub/Sub Message Bus** — In-process event bus replacing manual SQLite polling
- **Recovery Engine** — Periodic state checkpoints for crash resilience
- **FUSE Filesystem** — Virtual semantic directory structure (`~/semantic/`) for file browsing
- **Comprehensive Test Harness** — 742+ tests with quick/full/e2e/chaos/soak/gate scopes
- **Security Scanning** — Bandit SAST, pip-audit SCA, regex secret scan, 15-probe DAST
- **systemd Integration** — User-level targets and services for reliable daemon management
- **Packaging** — Electron-Builder with AppImage and .deb output

### Security
- 0 committed secrets across 24,700 files
- DAST sweep clean (15 probes, no 5xx or crashes)
- 9 HIGH Bandit findings under audit (controlled subprocess calls)
- 65 dependency CVEs identified for remediation (dev-only, not shipped)

### Known Limitations
- Linux only (no Windows or macOS support)
- Voice input relies on Chromium web-speech (native STT deferred)
- Docker deployment not recommended (requires systemd and window manager access)
- Dependency CVE cleanup in progress
- Subprocess security audit in progress
