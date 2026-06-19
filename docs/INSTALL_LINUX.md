# Install Guide — Linux

> **Beta Disclaimer:** Anion is in private beta. Installation requires technical Linux knowledge. Expect rough edges.

---

## System Requirements

| Requirement | Details |
|:---|:---|
| **OS** | Linux (Ubuntu, Fedora, Arch, etc.) |
| **Desktop** | X11, Sway, or i3 |
| **Python** | 3.11+ |
| **Node.js** | 18+ |
| **Ollama** | Installed and running |
| **systemd** | User services enabled |
| **Optional** | FUSE, `wmctrl`, `xdotool`, `playerctl` |

## Prerequisites

```bash
# Verify Python
python3 --version  # Should be 3.11+

# Verify Node.js
node --version     # Should be 18+

# Verify Ollama
ollama --version   # Should be installed and running

# Verify systemd
systemctl --user status  # Should not error

# Install desktop tools (Ubuntu/Debian)
sudo apt install wmctrl xdotool playerctl
```

## Installation

### Step 1: Install Backend Services

```bash
./scripts/anion install-services --apply
```

> Verify before publishing: Exact path assumptions.

### Step 2: Install Desktop App

**Option A: Debian Package (.deb) — Recommended**

```bash
sudo apt install ./ui/anion-shell/release/anion_0.1.0_arm64.deb
# Replace arm64 with amd64 for x64 systems
```

**Option B: Portable AppImage**

```bash
chmod +x ./ui/anion-shell/release/Anion-0.1.0-arm64.AppImage
./ui/anion-shell/release/Anion-0.1.0-arm64.AppImage
```

## Starting Anion

```bash
# Start all background services
./scripts/anion up

# Launch the desktop UI
# If installed via .deb: open "Anion" from your application launcher
# If using AppImage: run the AppImage file
```

## Stopping Anion

```bash
./scripts/anion down
```

## Checking Status

```bash
./scripts/anion status
```

## Viewing Logs

```bash
./scripts/anion logs --follow
```

## Diagnostics

```bash
./scripts/anion doctor
```

## Uninstall

```bash
# 1. Stop services
./scripts/anion down

# 2. Remove systemd services
./scripts/anion uninstall-services

# 3. Remove desktop app
sudo apt remove anion          # If installed via .deb
# Or delete the AppImage file  # If using AppImage

# 4. Delete user data (optional)
rm -rf ~/.anion
```

## Troubleshooting

| Issue | Solution |
|:---|:---|
| `systemctl` not available | Ensure you're on a systemd-based distro |
| Ollama not responding | Run `ollama serve` or check the Ollama service |
| Port 9120 in use | Check for other services: `ss -tlnp \| grep 9120` |
| FUSE mount fails | Install fuse: `sudo apt install fuse` |
| Permission denied on scripts | `chmod +x ./scripts/anion` |
