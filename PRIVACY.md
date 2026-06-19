# Privacy Policy

**Effective Date:** June 2026
**Project:** Anion — A local AI operating layer for the Linux desktop

> This policy is provided for transparency and should be reviewed before public launch.

---

## 1. Project Identity

Anion is a locally operated AI assistant layer for the Linux desktop. It is developed and maintained by Gopal Singh Rajput. Anion is currently in private beta.

## 2. What This Website / Beta Form Collects

If you apply for beta access via our application form:

- **Name** (optional)
- **Email address** (for communication about beta access)
- **Linux distribution and desktop environment** (to assess compatibility)
- **Interest description** (why you want to try Anion)

The beta application form is hosted on **Google Forms**. Data submitted through Google Forms is subject to [Google's Privacy Policy](https://policies.google.com/privacy). We use this data solely to evaluate beta eligibility and communicate access details.

## 3. What the Anion Application Processes Locally

When installed on your machine, Anion may process the following data **locally on your device**:

- Active window titles and workspace layout
- Terminal command history and error output
- Local file metadata (names, paths, modification times)
- Semantic memory entries (conversation fragments, pinned file contents)
- System performance metrics (CPU, memory usage)
- Cross-device sync payloads (encrypted end-to-end)

**All of this data is processed and stored locally.** Anion does not transmit this data to any remote server by default.

## 4. What Is NOT Collected

- Anion does **not** run cloud analytics or telemetry
- Anion does **not** phone home
- Anion does **not** collect usage statistics
- Anion does **not** share data with third parties
- No cookies are used by the desktop application

## 5. Local-First Design

Anion is architecturally local-first. AI inference is performed through [Ollama](https://ollama.ai), which runs entirely on your machine. Data stays on your device unless you explicitly configure cloud model fallback or cloud sync features.

## 6. Cross-Device Sync

If you enable cross-device sync, data is transferred directly between your devices over your local network using end-to-end encryption (NaCl Curve25519). No relay servers are involved in LAN sync mode.

If you opt into cloud sync (via Google account sign-in), sync data passes through Firebase infrastructure subject to Google's terms.

## 7. Analytics

Anion does not currently use any analytics, tracking, or telemetry services.

## 8. Data Retention

- **Beta form data:** Retained for the duration of the beta program. You may request deletion at any time.
- **Local application data:** Stored on your device in `~/.anion/`. You control this data entirely and can delete it at any time.

## 9. Data Sharing

Anion does not sell, share, or distribute your data to any third party.

## 10. User Deletion Requests

To request deletion of your beta application data, contact: [@GopalSinghRajput on GitHub](https://github.com/GopalSinghRajput)

To delete local application data, remove `~/.anion/` from your home directory.

## 11. Security

Anion binds its HTTP services exclusively to `127.0.0.1` (localhost). Network-facing exposure is limited to the optional cross-device sync feature, which uses end-to-end encryption. See [SECURITY.md](SECURITY.md) for details.

## 12. Children's Privacy

Anion is not designed for or directed at children under 13. We do not knowingly collect personal information from children.

## 13. International Users

Anion is developed and maintained from India. By using the beta application form, you consent to the processing of your data as described in this policy.

## 14. Changes to This Policy

This policy may be updated as Anion evolves. Material changes will be communicated through the beta program channels. The effective date at the top of this document reflects the latest revision.

## 15. Contact

For privacy-related inquiries: [@GopalSinghRajput on GitHub](https://github.com/GopalSinghRajput)

---

*This privacy policy covers both the Anion project website/beta form and the Anion desktop application.*
