# Roadmap

Anion's development priorities beyond v1, grouped by area.

---

## Public Beta Readiness

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P0 | Dependency CVE remediation | 65 known CVEs in dev dependencies need resolution | In progress |
| P0 | Subprocess security audit | 9 HIGH Bandit findings need input-provenance verification | In progress |
| P0 | Public documentation | Complete, accurate docs for beta users | In progress |
| P1 | CI security scanning | Automated lint on new findings | Planned |

## Safety and Security

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P0 | Hardened plugin sandbox | Current RLIMIT constraints are "lite"; real third-party execution needs namespaces | Planned |
| P1 | Input sanitization audit | Verify all subprocess calls use list-form args | In progress |
| P1 | File permission review | Ensure service files and configs have correct permissions | Planned |

## Packaging and Distribution

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P1 | Flatpak support | Better native integration on modern Linux distros than AppImage | Planned |
| P1 | Automated AppImage onboarding | First-run setup wizard for new users | Planned |
| P2 | ARM64 validation | Test on more ARM-based Linux systems | Planned |

## ARIA Improvements

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P1 | Native STT engine | Replace browser speech with `faster-whisper` for headless voice | Planned |
| P2 | Expanded tool set | Add more bounded tools based on user feedback | Planned |
| P2 | Multi-turn reasoning | Allow ARIA to maintain longer reasoning chains | Planned |

## Voice

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P1 | Offline wake word | Local wake-word detection (OpenWakeWord) | Planned |
| P1 | Streaming TTS | Chunk-based speech synthesis concurrent with text generation | Planned |

## Context and Memory

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P2 | Semantic graph expansion | Graph-based entity linking beyond vector search | Planned |
| P2 | Automatic memory pruning | Prevent unbounded database growth | Planned |
| P2 | Memory export/import | User-controlled data portability | Planned |

## Cross-Device Sync

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P1 | Full state file transfer | Sync actual files, not just metadata | Planned |
| P2 | Multi-device mesh | Support more than 2 devices | Planned |

## UI/UX

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P2 | Cross-device conflict UI polish | Better 3-way merge for complex state trees | Planned |
| P2 | Accessibility audit | Screen reader support, keyboard navigation | Planned |
| P2 | Theme customization | User-selectable color schemes | Planned |

## Developer Platform

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P2 | External skill SDK | Allow community devs to add tools to `TOOL_ALLOWLIST` securely | Planned |
| P2 | Plugin marketplace | Curated tool extensions | Planned |

## Performance

| Priority | Item | Why it matters | Status |
|:---|:---|:---|:---|
| P2 | Rust IPC rewrites | Replace heavy Python subprocess calls for OS IPC with Rust | Planned |
| P2 | Memory optimization | Reduce daemon memory footprint | Planned |
