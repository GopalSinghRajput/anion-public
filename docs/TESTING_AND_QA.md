# Testing and Quality Assurance

Anion's approach to testing, security scanning, and release readiness.

---

## Test Philosophy

Every backend change must pass the test gate before release. The test harness is designed to catch:

- Regressions in core functionality
- Security vulnerabilities
- Performance degradations
- System stability issues under stress

Tests are run via the unified `scripts/anion test` command.

## Test Harness

| Scope | Purpose | Duration |
|:---|:---|:---|
| `quick` | Smoke checks — basic health verification | < 2 min |
| `full` | Full regression suite (health + UI + assistant + safety + perf) | ~10 min |
| `e2e` | End-to-end validation with simulated interactions | ~15 min |
| `chaos` | Failure-state testing (degraded services, resource limits) | ~20 min |
| `soak` | Long-running stability test for memory leaks | 1–24 hours |
| `gate` | Release readiness check (returns READY/BLOCKED) | ~15 min |

## Test Coverage

- **742+ passing tests** across 162 test files
- Coverage areas include:
  - Backend API routes and state management
  - ARIA agentic loop and tool dispatch
  - Terminal intelligence (history, recovery, preview, tools)
  - Cross-device sync (crypto, pairing, timeline, transport)
  - UI snapshot contracts
  - Security guardrails and sandbox
  - Model hub and routing logic
  - Phase-based integration tests

## Security Scanning

### SAST (Bandit)

**Tool:** Bandit 1.9.4
**Scope:** Python source code (95,226 lines)

| Severity | Count | Notes |
|:---|:---|:---|
| HIGH | 9 | 5× `os.system` in desktop launcher, 4× `subprocess(shell=True)` in controlled contexts |
| MEDIUM | 170 | Import checks, SQL construction, random module usage |
| LOW | 1,543 | Informational findings |

The 9 HIGH findings are under audit. All involve operator-controlled inputs (not user-controlled). None have demonstrated exploitability, but fixes are in progress.

### SCA (pip-audit)

**Tool:** pip-audit 2.10.0
**Scope:** Python virtual environment (202 packages)

- **65 known CVEs** across 17 packages
- These exist in the dev virtual environment only, not in shipped production artifacts
- Priority packages for remediation: `cryptography`, `urllib3`, `jinja2`, `paramiko`

### Secret Scanning

**Method:** Regex sweep across `git ls-files`
**Scope:** 24,700 files

- **0 findings** — No committed API keys, tokens, passwords, or PEM keys

### DAST

**Tool:** Custom `dast_scanner.py` with 15 active probes
**Scope:** HTTP bridge on `127.0.0.1:9120`

Probes include: path traversal, oversized JSON, malformed bodies, header smuggling, method abuse, oversized URL, NUL byte injection, unknown content-type.

- **0 findings** — All probes return appropriate responses (404/400/501). No 5xx errors, no parser crashes, no timeouts.

## Soak Testing

24-hour stability tests verify:
- No memory leaks in daemon processes
- Stable response times under sustained load
- No database corruption under continuous writes
- Service restart resilience

## Release Gate Process

The `scripts/anion test gate` command runs a comprehensive check:

1. Full test suite (742+ tests)
2. Manifest validation (all required files present)
3. Import checks (core modules load cleanly)
4. Doctor checks (system health)

Exit codes:
- `0` — READY for release
- `2` — NOT READY (test failures)
- `3` — BLOCKED (critical issues)

## What Remains

- Dependency CVE remediation (pip-audit findings)
- Subprocess security hardening (Bandit HIGH findings)
- CI integration for automated security scanning
- Additional e2e test scenarios for cross-device sync
