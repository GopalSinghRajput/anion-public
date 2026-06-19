# Security Policy

## Supported Versions

Anion is currently in **private beta**. Only the latest release candidate is supported.

| Version | Supported |
|:---|:---|
| v0.1.x (current RC) | ✅ Active |
| Earlier builds | ❌ Not supported |

## Reporting a Vulnerability

If you discover a security vulnerability in Anion, **do not open a public GitHub issue.**

Instead, please report it privately:

- **GitHub:** Open a [Security Advisory](https://github.com/GopalSinghRajput/anion/security/advisories/new)
- Or contact [@GopalSinghRajput](https://github.com/GopalSinghRajput) directly

Please include:
- A description of the vulnerability
- Steps to reproduce (if applicable)
- The potential impact
- Any suggested mitigations

## Response Timeline

We aim to acknowledge security reports within **48 hours** and provide an initial assessment within **7 days**.

## Responsible Disclosure

We follow responsible disclosure practices:

1. **Report privately** via the contact above
2. Allow reasonable time for investigation and remediation
3. We will credit reporters (with permission) in release notes
4. Please do not publicly disclose vulnerabilities before a fix is available

## What to Report

- Authentication or authorization bypasses
- Remote code execution vectors
- Data exposure or leakage
- Privilege escalation
- Denial of service vulnerabilities
- Cryptographic weaknesses in the sync protocol

## What NOT to Report Publicly

- Do not file public issues for security vulnerabilities
- Do not share exploit code publicly before a fix is released
- Do not test against other users' installations

## Local Services Security

Anion's HTTP bridge binds exclusively to `127.0.0.1:9120`. It is not designed to be network-accessible. If you expose this port externally, you do so at your own risk.

## ARIA Tool Safety

ARIA operates within a strict `TOOL_ALLOWLIST` of 22 predefined tools. Each tool has:

- A defined JSON schema with type validation
- A risk tier classification (`low`, `medium`, `high`)
- Approval gates for sensitive operations

ARIA cannot execute arbitrary shell commands. High-risk actions require explicit user approval through the UI.

## Known Beta Hardening Areas

The following areas are actively being hardened:

### Dependency CVEs
- 65 known CVEs across 17 packages in the development virtual environment
- These are dev-only dependencies, not shipped in production artifacts
- Priority packages: `cryptography`, `urllib3`, `jinja2`, `paramiko`

### Subprocess Findings
- 9 HIGH findings from Bandit SAST scanning
- 5× `os.system()` calls in desktop app launcher (controlled inputs)
- 4× `subprocess(shell=True)` calls in controlled contexts
- Input provenance audit in progress

### Packaging Validation
- AppImage and .deb packaging under validation
- Service file permissions being reviewed
- Hardcoded path elimination in progress

## Security Scanning

Anion's test harness includes automated security scanning:

| Tool | Scope | Status |
|:---|:---|:---|
| Bandit (SAST) | Python source code | ✅ Running |
| pip-audit (SCA) | Python dependencies | ✅ Running |
| Secret scan | Full git tree (24,700 files) | ✅ Clean (0 findings) |
| DAST scanner | HTTP bridge (15 probes) | ✅ Clean |

## Contact

For security reports: Open a [GitHub Security Advisory](https://github.com/GopalSinghRajput/anion/security/advisories/new) or contact [@GopalSinghRajput](https://github.com/GopalSinghRajput).
