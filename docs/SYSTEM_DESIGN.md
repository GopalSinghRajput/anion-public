# System Design

## Problem Statement

Modern Linux power users juggle between terminals, file managers, web browsers, and AI chat interfaces. Each tool operates in isolation — the AI doesn't know what's on your screen, your terminal doesn't learn from past errors, and switching between devices means losing context.

Anion solves this by creating a unified AI layer that lives on the OS level, continuously observing desktop state, terminal activity, and file changes to provide context-aware assistance.

## Design Goals

1. **Local-first privacy** — All AI processing happens on-device via Ollama. No data leaves the machine by default.
2. **Deep OS integration** — Leverage Linux-specific capabilities (systemd, FUSE, WM IPC) for genuine desktop awareness.
3. **Bounded agentic AI** — Give the assistant real capabilities but with strict safety guardrails.
4. **Real-time responsiveness** — Stream state changes to the UI instantly via SSE.
5. **Crash resilience** — Backend survives UI crashes; recovery checkpoints protect against daemon failures.

## Non-Goals

1. **Cross-platform support** — Anion is Linux-only by design. The depth of OS integration makes cross-platform infeasible without significant compromise.
2. **Cloud-first architecture** — Anion is not a cloud service with a desktop client. It's a local system with optional cloud features.
3. **Consumer polish** — The current focus is technical depth and reliability, not onboarding UX for non-technical users.
4. **Docker deployment** — Docker containers cannot access systemd user services, FUSE mounts, or window manager IPC.

---

## Key Design Decisions

### Why Linux-Only

Anion's core value comes from deep OS integration:
- **systemd user services** for reliable daemon management
- **FUSE** for transparent filesystem awareness
- **WM IPC** (Sway, i3, X11) for live window context
- **D-Bus** for desktop search integration

These capabilities don't exist on Windows or macOS in equivalent forms. Building for Linux means Anion can be a genuine OS layer rather than a generic app.

### Why Local-First

User data sovereignty is a core principle:
- Terminal history stays on-device
- File contents are never uploaded
- AI inference runs locally via Ollama
- Cross-device sync uses E2E encryption

Users who choose cloud model fallback do so explicitly, and their data passes through their own Ollama daemon — Anion never handles API keys.

### Why Ollama

Ollama provides:
- Simple local model management
- Fast inference on consumer hardware
- Growing model ecosystem
- Optional cloud compute (handled by Ollama, not Anion)

Anion remains model-agnostic — it sends prompts to Ollama and receives responses. The user controls which models are available.

### Why systemd Services

Background daemons need reliable lifecycle management:
- Automatic restart on failure
- Clean startup/shutdown ordering via targets
- User-level scope (no root required)
- Standard logging via journald
- Integration with system boot/login

### Why Electron/React Shell

The UI needs:
- WebGL for Three.js Brain visualization
- Rich component ecosystem (React)
- Desktop window management (Electron)
- Fast development iteration (Vite + HMR)

The Electron pivot came after evaluating Qt/QML (limited WebGL support) and Tauri (insufficient Node IPC capabilities for the required desktop integration depth).

### Why Python Backend

Python was chosen for:
- Rapid prototyping of AI integration patterns
- Rich ecosystem for NLP, file processing, and system interaction
- SQLite bindings with WAL mode support
- FUSE bindings (`fusepy`)
- subprocess management for WM IPC

### Why SSE Instead of Polling

Server-Sent Events provide:
- Real-time state updates without client polling
- Lower latency than REST polling loops
- Simpler implementation than WebSockets for unidirectional flow
- Natural fit for "backend pushes, frontend renders" architecture

### Why ARIA Tools Are Bounded

Unbounded AI tool use is dangerous:
- LLMs can hallucinate tool calls
- Arbitrary shell access could cause damage
- Users need confidence that the AI won't surprise them

ARIA's `TOOL_ALLOWLIST` defines exactly 22 tools. Each has a JSON schema, risk tier, and validation logic. New tools require explicit addition through a defined process.

### Why Docker Is Not Recommended

Anion requires:
- `systemctl --user` (not available in containers)
- FUSE mounts (requires `--privileged`)
- Window manager IPC (requires host display access)
- D-Bus session bus (requires host bus access)

Running Anion in Docker would require so many host-access workarounds that it defeats the purpose of containerization.

---

## Security and Privacy Tradeoffs

| Design Choice | Security Benefit | Tradeoff |
|:---|:---|:---|
| Local-first inference | Data never leaves device | Requires local compute resources |
| Tool allowlist | Prevents arbitrary execution | Limits ARIA's flexibility |
| Approval gates | User controls sensitive actions | Interrupts autonomous flows |
| localhost binding | No network exposure | Cannot serve remote clients |
| Privacy redactor | Screens cloud prompts | May over-redact, reducing quality |
| RLIMIT sandbox | Constrains resource usage | Plugin capabilities limited |

## Packaging Tradeoffs

| Format | Pros | Cons |
|:---|:---|:---|
| AppImage | Single portable binary, no root needed | Large bundle (~100MB), no auto-updates |
| .deb | Native package management, dependency handling | Distro-specific, requires sudo |
| Flatpak (planned) | Sandboxed, auto-updates, distro-agnostic | Requires portal integration for system access |

---

## Tradeoff Table

| Decision | Why chosen | Tradeoff |
|:---|:---|:---|
| Linux-only | Needed real desktop/system context | No Windows/macOS support |
| Local-first models | Privacy and offline workflow | User needs local compute |
| systemd services | Reliable daemon management | Linux-specific |
| Electron shell | Rich desktop UI with WebGL | Larger bundle size |
| SSE bridge | Real-time backend updates | Requires local service health |
| Python backend | Rapid AI integration development | Lower performance than Rust/Go |
| SQLite WAL | Simple, reliable local storage | Single-machine only |
| NaCl Curve25519 | Strong E2E encryption | Custom protocol complexity |
| Bounded tools | Safe agentic behavior | Limited assistant flexibility |

---

## Lessons Learned

1. **Qt/QML → Electron was the right call.** WebGL (Three.js) is essential for the Brain visualization, and React's component ecosystem accelerated UI development significantly.

2. **Tauri → Electron was necessary.** Tauri's Rust backend couldn't support the heavy Node IPC patterns needed for Electron's deep desktop integration hooks.

3. **SSE >> polling.** Moving from REST polling to SSE eliminated an entire class of timing bugs and reduced UI latency dramatically.

4. **Tool allowlists are essential.** Early experiments with unconstrained tool use showed that LLMs will hallucinate tool calls. The allowlist solved this completely.

5. **WAL mode is non-negotiable.** SQLite contention between the memory engine, context tracker, and FUSE watcher caused data loss until WAL mode was enabled globally.

6. **Security scanning must be automated.** Manual security reviews miss things. Bandit + pip-audit + DAST in the test harness catches regressions before they ship.
