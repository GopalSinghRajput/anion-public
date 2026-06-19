# Feature Breakdown

A complete inventory of Anion's implemented features, grouped by subsystem.

---

## Desktop Shell

### ARIA Widget Dashboard
**What it does:** Primary landing page with interactive widget grid and media player.
**User value:** Centralized dashboard for all Anion interactions.
**Technical approach:** React components consuming SSE state from Python backend.
**Current status:** Implemented

### Live Neural Brain
**What it does:** Three.js holographic visualization pulsing with system load.
**User value:** Intuitive at-a-glance system state understanding.
**Technical approach:** Three.js WebGL in Electron, driven by real-time health data.
**Current status:** Implemented

### Ambient Presence Bar
**What it does:** Lightweight top-bar showing live system state.
**User value:** Non-intrusive monitoring without opening the full dashboard.
**Technical approach:** Electron overlay window consuming SSE health stream.
**Current status:** Implemented

### Dynamic Continuity Context
**What it does:** Real-time unfinished work and triage suggestions.
**User value:** Never lose track of what you were working on.
**Technical approach:** Backend triage engine pushes continuity cards via SSE.
**Current status:** Implemented

### Conflict Resolution Modal
**What it does:** 3-way merge UI for cross-device state collisions.
**User value:** Clear resolution of conflicting changes across devices.
**Current status:** Implemented

---

## ARIA Assistant

### Agentic Tool Calling
**What it does:** 22 strictly defined tools with capability gating and approval gates.
**User value:** ARIA takes real actions while remaining safe.
**Technical approach:** ReAct loop with JSON tool schemas, `TOOL_ALLOWLIST`, `RISK_TIERS`.
**Current status:** Implemented

### Privacy Redaction
**What it does:** Screens prompts before routing to cloud models.
**User value:** Cloud model use doesn't leak private data.
**Technical approach:** `PrivacyRedactor` with pattern matching; sensitive prompts fall back to local models.
**Current status:** Implemented

### Token Streaming
**What it does:** Real-time text generation streamed via SSE.
**User value:** Instant feedback rather than waiting for complete responses.
**Current status:** Implemented

### Dynamic Suggestions v2
**What it does:** Context-aware UI nudges based on user activity patterns.
**User value:** Proactive assistance without manual invocation.
**Technical approach:** Feature Activation Engine with context triggers and dynamic policy refinement.
**Current status:** Implemented

### Voice Interaction
**What it does:** Voice input and TTS for ARIA conversations.
**User value:** Hands-free interaction with the assistant.
**Technical approach:** Browser-based speech recognition via Chromium APIs. TTS via backend voice pipeline.
**Current status:** Implemented (browser-based; native STT deferred)

---

## Terminal Intelligence

### Persistent Command History
**What it does:** SQLite-backed command history surviving restarts.
**User value:** Never lose command history; searchable across sessions.
**Current status:** Implemented

### Risk Preview
**What it does:** Deterministic scanning for destructive commands.
**User value:** Safety net preventing accidental `rm -rf`.
**Technical approach:** Pattern matching against destructive signatures; execution paused until confirmed.
**Current status:** Implemented

### Auto-Fix Recovery
**What it does:** Instant diagnosis and fix suggestions for CLI errors.
**User value:** Solve `ModuleNotFoundError` without manual searching.
**Technical approach:** Hybrid rule-based engine with LLM fallback for complex errors.
**Current status:** Implemented

---

## Context and Memory

### Desktop Window Context
**What it does:** Captures active window titles, workspace layout, and geometry.
**User value:** ARIA understands what apps you're using.
**Technical approach:** Abstraction layer wrapping `wmctrl`, `xdotool`, `swaymsg`, `i3-msg`.
**Current status:** Implemented

### Semantic Memory Store
**What it does:** Persistent memory of interactions and semantic history.
**User value:** ARIA remembers past conversations.
**Technical approach:** SQLite WAL with FTS5 full-text search indexes.
**Current status:** Implemented

### Pinned Files
**What it does:** Attach local files to the LLM context.
**User value:** Ask ARIA questions about specific documents.
**Current status:** Implemented

### Unified Semantic Ranking
**What it does:** 7-factor scoring engine for search results.
**User value:** More relevant results than keyword matching.
**Current status:** Implemented

---

## File/Workspace Awareness

### FUSE Semantic Filesystem
**What it does:** Virtual directory at `~/semantic/` with AI-organized views.
**User value:** Browse AI-categorized files in standard file managers.
**Technical approach:** FUSE filesystem exposing search, thread, and time-based directories.
**Current status:** Implemented

### Filesystem Event Watching
**What it does:** Real-time file change monitoring.
**User value:** Context stays current with file modifications.
**Current status:** Implemented

---

## Cross-Device Sync

### LAN Discovery & Pairing
**What it does:** Discovers Anion instances via UDP broadcasts; pairs with 6-digit PIN.
**User value:** Automatic device discovery without manual config.
**Current status:** Implemented

### E2E Encrypted Sync
**What it does:** Secure state transfer using NaCl Curve25519.
**User value:** Cross-device continuity without exposing data to third parties.
**Current status:** Implemented

---

## Testing and Diagnostics

### Comprehensive Test Harness
**What it does:** 742+ tests with quick/full/e2e/chaos/soak/gate scopes.
**User value:** High confidence in system reliability.
**Current status:** Implemented

### Security Scanning
**What it does:** Automated SAST, SCA, secret scanning, and DAST.
**User value:** Known security posture before every release.
**Current status:** Implemented

---

## Packaging

### AppImage & .deb Distribution
**What it does:** Portable binary (AppImage) and native Debian package.
**User value:** Multiple install options for different preferences.
**Current status:** Implemented

### Plugin Sandbox-Lite
**What it does:** RLIMIT constraints (memory, CPU, FD) for plugin execution.
**User value:** Plugins cannot consume excessive resources.
**Current status:** Implemented
