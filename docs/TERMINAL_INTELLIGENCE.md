# Terminal Intelligence

Anion's terminal intelligence system upgrades the standard CLI experience with persistent history, safety features, and automatic error recovery.

---

## Overview

The terminal intelligence module (`anion_term/`) wraps the traditional command-line interface to add:

- **Persistent command history** that survives restarts
- **Risk previews** that catch destructive commands before execution
- **Auto-fix recovery** that instantly diagnoses common errors

These features work alongside the standard shell — they augment rather than replace your existing terminal workflow.

---

## Command Wrapper

The terminal wrapper intercepts commands to provide intelligence features:

1. **Pre-execution**: Scans the command for destructive patterns (risk preview)
2. **Execution**: Runs the command normally
3. **Post-execution**: Captures output and errors for recovery analysis
4. **History**: Logs the command to persistent SQLite storage

## Persistent Command History

Unlike shell history files that can be lost or corrupted, Anion stores command history in a SQLite database:

- Survives terminal restarts and system reboots
- Searchable across all sessions
- Includes timestamps, exit codes, and working directories
- Accessible to ARIA for context-aware assistance

## Recovery Suggestions

When a command fails, the recovery system provides instant fix suggestions:

### What Is Deterministic (Rule-Based)

Common error patterns are handled instantly without LLM calls:

| Error Pattern | Instant Suggestion |
|:---|:---|
| `ModuleNotFoundError: No module named 'requests'` | `pip install requests` |
| `command not found: node` | `sudo apt install nodejs` |
| `Permission denied` | `sudo !!` or `chmod +x ./script.sh` |
| `No such file or directory` | Check spelling, suggest `find` |

### What Is LLM-Assisted

For complex errors that don't match known patterns, the system falls back to asking the local Ollama model for diagnosis. This provides:

- Contextual explanation of the error
- Step-by-step fix suggestions
- Related documentation references

## Risk Preview

The risk preview system is **fully deterministic** — no LLM is involved. It scans commands against a set of known destructive patterns:

### Common Patterns Caught

| Command Pattern | Risk Level | Action |
|:---|:---|:---|
| `rm -rf /` or `rm -rf ~` | Critical | Block and require confirmation |
| `rm -rf *` | High | Pause and warn |
| `chmod -R 777` | Medium | Display warning |
| `dd if=... of=/dev/...` | Critical | Block and require confirmation |
| `mkfs.*` | Critical | Block and require confirmation |
| `:(){:\|:&};:` | Critical | Block (fork bomb) |

### How It Works

1. Command is intercepted before execution
2. Pattern matcher scans for destructive signatures
3. If matched, execution is **paused**
4. User sees a clear warning with the risk assessment
5. User must explicitly confirm to proceed

### Example Flow

```
$ rm -rf ~/Documents

⚠️  DESTRUCTIVE COMMAND DETECTED
    Command: rm -rf ~/Documents
    Risk: HIGH — Recursive forced deletion of user directory
    
    This will permanently delete all files in ~/Documents.
    
    [y] Confirm  [n] Cancel  [e] Edit command
```

## Destructive Command Confirmation

The confirmation prompt requires explicit user input. Default behavior is to **cancel** — the user must actively choose to proceed. This prevents accidental execution of dangerous commands.

## Safety Boundaries

The terminal intelligence system has clear boundaries:

- **It does not prevent all dangerous commands** — only known destructive patterns
- **It is not a security sandbox** — it's a safety net for accidents
- **It does not modify commands** — it only warns and pauses
- **It respects user autonomy** — confirmed commands always execute
- **LLM recovery suggestions are suggestions only** — they are never auto-executed

## Example Flows

### Auto-Recovery Example

```
$ python3 app.py
Traceback (most recent call last):
  File "app.py", line 1, in <module>
    import flask
ModuleNotFoundError: No module named 'flask'

💡 Quick fix: pip install flask
   [Enter] to apply  [n] to skip
```

### Risk Preview Example

```
$ sudo chmod -R 777 /etc

⚠️  RISKY COMMAND DETECTED
    Command: sudo chmod -R 777 /etc
    Risk: HIGH — Setting world-writable permissions on system directory
    
    [y] Confirm  [n] Cancel
```

### History Search Example

```
$ anion history search "docker"

Results:
  [2026-06-15 14:32] docker build -t myapp .          (exit 0)
  [2026-06-15 14:35] docker run -p 8080:80 myapp      (exit 0)
  [2026-06-14 09:12] docker compose up -d             (exit 1)
```
