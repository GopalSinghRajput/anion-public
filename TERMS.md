# Terms of Use

**Effective Date:** June 2026
**Project:** Anion — A local AI operating layer for the Linux desktop

---

## 1. Beta Status

Anion is currently in **private beta**. The software is provided as a release candidate for testing and evaluation purposes. It is not yet considered production-ready.

## 2. Platform Scope

Anion is designed exclusively for **Linux** desktop systems. It requires systemd, FUSE support, and compatible window managers (X11/Sway/i3). It is not supported on Windows or macOS.

## 3. Source Code

The Anion source code is **private** during the beta and security hardening phase. This public repository contains documentation, architecture descriptions, and product information only. Anion is not open source at this time.

## 4. No Warranty

Anion is provided "as is" without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement.

## 5. User Responsibility

By installing and running Anion, you acknowledge that:

- Anion integrates deeply with your Linux system (systemd services, FUSE mounts, window manager IPC)
- Anion runs background daemons that consume system resources
- You are responsible for ensuring your system meets the documented requirements
- You should review destructive actions even when the terminal intelligence feature provides safety prompts

## 6. Local Services and System Integration

Anion installs and manages user-level systemd services. These services:

- Run under your user account (not root)
- Bind HTTP services to `127.0.0.1` only
- Use local SQLite databases for data storage
- Interact with your window manager for desktop context

You should be comfortable with background services running on your system before installing Anion.

## 7. Safe Use

- Do not feed intentionally malicious inputs to the ARIA assistant or terminal wrapper
- Do not expose the local HTTP bridge (port 9120) to external networks
- Do not bypass the tool allowlist or guardrail mechanisms

## 8. Beta Access

Beta access is granted at the discretion of the project maintainer. Access may be revoked at any time for any reason, including but not limited to:

- Misuse of the software
- Violation of these terms
- Security concerns

## 9. Feedback

By providing feedback during the beta program, you grant the Anion project permission to use that feedback to improve the product. You retain ownership of your feedback content.

## 10. Downloads and Installers

If distributable installers (AppImage, .deb) are provided, they are for evaluation purposes during the beta period. Redistribution of Anion installers without permission is prohibited.

## 11. Limitation of Liability

In no event shall the Anion project or its contributors be liable for any claim, damages, or other liability arising from or related to the use of the software. This includes but is not limited to data loss, system instability, or service interruptions.

## 12. Privacy

Your privacy is important. See our [Privacy Policy](PRIVACY.md) for details on data handling.

## 13. Changes

These terms may be updated as Anion evolves. Changes will be communicated through beta program channels.

## 14. Contact

For questions about these terms: [@GopalSinghRajput on GitHub](https://github.com/GopalSinghRajput)
