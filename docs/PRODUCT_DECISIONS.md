# Product Decisions

The reasoning behind Anion's major product and technical decisions.

---

## Linux-Only

**Decision:** Build exclusively for Linux.

**Why:** Anion's value comes from deep OS integration — systemd services, FUSE mounts, window manager IPC, D-Bus. These are Linux-specific capabilities. A cross-platform build would require abandoning most of what makes Anion useful.

**Consequence:** No Windows or macOS support. This limits the user base but enables a depth of integration that generic cross-platform apps cannot achieve.

## Local-First

**Decision:** All AI processing happens on-device by default.

**Why:** User data sovereignty. Terminal history, file contents, and desktop context are deeply personal. Sending this to cloud APIs creates privacy and security risks that conflict with the project's values.

**Consequence:** Users need local compute resources to run Ollama models. Cloud fallback is available but optional and goes through the user's own Ollama daemon.

## The Electron Pivot

**Evidence:** The project started with Qt/QML prototypes before moving to Electron/React.

**Why Electron won:**
- WebGL support needed for Three.js Brain visualization
- React component ecosystem for rapid UI development
- Vite HMR for fast iteration cycles
- Electron's Node IPC for deep desktop integration

**What was lost:** Smaller binary size (Qt), native look and feel.

## The Qt/QML Detour

**Evidence:** Phase 14 documentation references a substantial QML design token system.

**What happened:** A significant UX overhaul was built in Qt/QML with strict design tokens. It worked well but couldn't support the WebGL visualization requirements and had a steeper learning curve for UI iteration.

**Lesson:** Validate technical requirements before investing deeply in a UI framework.

## The Tauri Detour

**Evidence:** `ui/anion-shell/README.md` references Tauri template origins.

**What happened:** Tauri was evaluated as a lighter alternative to Electron. However, Tauri's Rust backend couldn't support the heavy Node IPC dependencies needed for Anion's desktop integration depth.

**Lesson:** Lighter isn't always better. The specific IPC patterns Anion needed were only well-served by Electron's architecture.

## Docker Not Recommended

**Decision:** Docker is explicitly not a recommended deployment target.

**Why:** Anion requires:
- `systemctl --user` (not available in containers)
- FUSE mounts (requires `--privileged`)
- Window manager IPC (requires host display)
- D-Bus session bus (requires host bus)

Running Anion in Docker would require so many host-access workarounds that containerization provides no practical benefit.

## Security Hardening Decisions

**Decision:** Keep the source private during beta.

**Why:** Known security debts (dependency CVEs, subprocess findings) create risk if exposed publicly before remediation. Responsible disclosure means fixing known issues before making the attack surface visible.

**Plan:** Open-source after completing the security cleanup pass.

## Why the Source Remains Private

1. 65 known dependency CVEs need remediation
2. 9 subprocess findings need audit
3. Packaging validation is incomplete
4. Public documentation is being finalized

The architecture, features, and technical approach are documented publicly in this repository. The implementation code will follow once the security posture is satisfactory.

## Beta Positioning

**Decision:** Position Anion as a private beta / release candidate.

**Why:** The system is technically feature-complete but not consumer-ready. It requires:
- Technical Linux knowledge to install and configure
- Ollama installed and running
- Comfort with systemd services and terminal workflows

Marketing it as "production-ready" would be dishonest. Positioning it as a beta sets appropriate expectations.

## Final v1 Scope

Anion v1 includes:
- ✅ Agentic assistant (ARIA) with bounded tools
- ✅ Terminal intelligence (history, recovery, risk preview)
- ✅ Context and memory engine
- ✅ Cross-device encrypted sync
- ✅ Live desktop shell with Brain visualization
- ✅ systemd daemon architecture
- ✅ Comprehensive test harness (742+ tests)
- ✅ Security scanning (SAST, SCA, DAST)
- ✅ Packaging (AppImage + .deb)

Explicitly deferred to v2:
- ❌ Native STT engine (using browser speech for now)
- ❌ Hardened plugin namespace sandbox (using RLIMIT for now)
- ❌ Full file transfer in cross-device sync
- ❌ External skill SDK for community tools
- ❌ Flatpak packaging
