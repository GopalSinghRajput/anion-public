# Frequently Asked Questions

---

## General

**What is Anion?**
A privacy-first, local AI operating layer for the Linux desktop. It provides an agentic assistant (ARIA), terminal intelligence, context-aware memory, and cross-device sync — all running locally on your machine.

**Is Anion available for Windows or macOS?**
No. Anion relies on Linux-specific tools like systemd user services, FUSE, and X11/Wayland integrations. Cross-platform support is not planned.

**Is Anion open source?**
Not yet. The source code is private during beta and security hardening. This repository provides public documentation of the architecture and features. The plan is to open-source after the security cleanup.

**Is Anion production-ready?**
No. It is a release candidate / private beta. Expect rough edges and known limitations.

---

## Technical

**Does Anion require internet?**
No. The entire AI architecture runs offline using Ollama. Internet is only needed if you explicitly ask ARIA to search the web.

**Does Anion send my files to the cloud?**
No. It operates locally by default. Cloud model fallback is optional and routes through your own Ollama daemon.

**Do I need Ollama?**
Yes. Ollama is the underlying engine Anion uses for local LLM inference.

**How does Ollama Cloud authentication work?**
Anion never handles API keys or cloud credentials. When you select a cloud model, Anion sends the request to your local `ollama` daemon, which handles all authentication (via `ollama login`). Anion remains blind to your credentials.

**Can ARIA run shell commands?**
No. ARIA has a restricted toolset of 22 tools. It cannot open a shell or run arbitrary commands.

**Can ARIA delete files?**
No. The system refuses high-risk autonomous actions without explicit approval.

**Why does Anion need systemd?**
To reliably manage background daemons, file watchers, and memory engines independently of the desktop UI.

**Why does Anion need `wmctrl` or `xdotool`?**
To capture your active window title and layout context for the AI.

**Can I run Anion in Docker?**
Not recommended. Anion needs deep access to your active desktop session (systemd, FUSE, window manager IPC).

---

## Operations

**How do I view logs?**
```bash
./scripts/anion logs --follow
```

**How do I check system health?**
```bash
./scripts/anion doctor
```

**What should I run before reporting a bug?**
Run `./scripts/anion doctor` and `./scripts/anion test quick` to gather system health info. Include the output in your bug report.

**How do I delete all Anion data?**
```bash
rm -rf ~/.anion
```

**How do I update Anion?**
```bash
./scripts/anion down
git pull
cd ui/anion-shell && npm install && cd ../..
./scripts/anion install-services
./scripts/anion up
```
