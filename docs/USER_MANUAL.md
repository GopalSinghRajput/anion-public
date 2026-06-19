# User Manual

## 1. What is Anion?

Anion is a privacy-first, local AI operating layer for the Linux desktop. It runs alongside your OS, understanding your workflow — active windows, terminal commands, and local files — to provide context-aware AI assistance.

It consists of:
- A **Python backend** running via systemd user services
- An **Electron/React desktop shell** (the Anion Shell)
- A **local HTTP/SSE bridge** for real-time communication
- **ARIA** — an agentic voice and text assistant powered by local Ollama models

## 2. Who Anion is For

- Linux desktop power users and developers
- Terminal-heavy users
- People comfortable running local AI models (Ollama)
- Users who prioritize privacy-first, local AI operations

## 3. Current Status

Anion v1 is a **Linux-only release candidate / private beta**. It is feature-complete but undergoing security hardening. Treat this as beta software.

## 4. System Requirements

- **OS:** Linux (X11, Sway, or i3)
- **Python:** 3.11+
- **Node.js:** 18+
- **AI Provider:** Ollama (installed and running)
- **System Services:** systemd user services enabled
- **File Integration:** FUSE (optional, for semantic filesystem)
- **Desktop Tools:** `wmctrl`, `xdotool` (X11) or `swaymsg`, `i3-msg` (Sway/i3)

## 5. Using ARIA

ARIA can:
- Set timers and reminders
- Open applications (VS Code, browser, terminal)
- Read pinned files and answer questions about them
- Perform web searches
- Track notes and to-do items

ARIA **cannot** run arbitrary shell commands or delete files. Sensitive actions require explicit approval.

## 6. Using Terminal Intelligence

- **Risk Previews:** Catches destructive commands (`rm -rf`) before execution
- **Auto-Fix Recovery:** Instant fix suggestions for errors like `ModuleNotFoundError`
- **Persistent History:** SQLite-backed history surviving restarts

## 7. Using Cross-Device Sync

Enable with: `mkdir -p ~/.anion/sync`

Devices pair via 6-digit PIN. All data encrypted with NaCl Curve25519.

If your router blocks UDP broadcasts (AP Isolation), use Cloud Sync via Google Account sign-in instead.

## 8. Troubleshooting

| Symptom | Fix |
|:---|:---|
| UI does not open | `cd ui/anion-shell && npm install` |
| Backend not running | `./scripts/anion status` then `./scripts/anion up` |
| UI stuck "connecting" | Check `./scripts/anion logs --follow` |
| Ollama errors | Ensure `ollama` service is active |
| Missing desktop context | Install `wmctrl` / `xdotool` |
| ARIA not responding | `./scripts/anion doctor` |

## 9. Glossary

- **ARIA** — Anion's agentic assistant
- **Ollama** — Local LLM inference engine
- **SSE** — Server-Sent Events (real-time data protocol)
- **FUSE** — Filesystem in Userspace
- **ReAct** — Reason-and-Act cognitive loop
- **Guardrail** — Safety interception code
