# Diagrams

This directory contains Mermaid diagram source files (`.mmd`) for Anion's architecture and workflows.

## Rendering

Mermaid diagrams can be rendered in several ways:

### GitHub
GitHub renders `.mmd` files automatically when embedded in markdown using fenced code blocks:

````markdown
```mermaid
flowchart TD
    A --> B
```
````

### VS Code
Install the [Mermaid Preview](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid) extension.

### CLI
Use the [Mermaid CLI](https://github.com/mermaid-js/mermaid-cli):

```bash
npx -y @mermaid-js/mermaid-cli mmdc -i architecture-overview.mmd -o architecture-overview.png
```

### Online
Paste diagram content into [mermaid.live](https://mermaid.live/) for interactive editing and export.

## Diagrams

| File | Description |
|:---|:---|
| `architecture-overview.mmd` | High-level system architecture |
| `aria-agent-flow.mmd` | ARIA ReAct agent sequence |
| `context-memory-flow.mmd` | Context and memory data flow |
| `cross-device-sync-flow.mmd` | Cross-device sync protocol |
| `terminal-intelligence-flow.mmd` | Terminal risk preview and recovery |
| `testing-pipeline.mmd` | Testing and release gate pipeline |
| `privacy-boundary.mmd` | Privacy redaction and tool safety |
