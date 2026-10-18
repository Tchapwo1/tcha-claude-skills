---
name: tcha-mcp-firewall
description: Real-time transport firewall and boundary enforcer for Model Context Protocol (MCP) servers and Claude tool execution. Blocks Cloud Metadata SSRF (169.254.169.254), path traversal (../../), and destructive system commands.
---

# Tcha MCP Firewall

In-line transport firewall standing between Claude (or any MCP host client) and tool execution servers. Enforces deterministic boundary policies in under 1 millisecond.

## Policy Enforcement Matrix

| Threat Vector | Attack Pattern | Firewall Action |
| :--- | :--- | :--- |
| **Cloud Metadata SSRF** | `http://169.254.169.254/...`, `metadata.google.internal` | **DENIED (403)** — IP range blocked |
| **Path Traversal** | `../../etc/passwd`, `..\..\Windows\System32` | **DENIED (403)** — Working root enforced |
| **Destructive Terminal** | `rm -rf /`, `mkfs`, `format`, `dd if=/dev/zero` | **DENIED (403)** — Blacklisted binary pattern |
| **Privilege Escalation** | `chmod 777`, `sudo`, `Set-ExecutionPolicy Bypass` | **DENIED (403)** — Strict user privilege ceiling |
| **Egress Exfiltration** | Outbound DNS/HTTP requests to unverified domains | **FLAGGED / QUARANTINED** |

## Configuration for Claude Desktop

Add Tcha as a proxy wrapper inside `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{
  "mcpServers": {
    "protected-tools": {
      "command": "npx",
      "args": ["-y", "tcha-protection", "guard", "--mcp"]
    }
  }
}
```

## Performance & Audit
- Interception Overhead: **0.42ms average**.
- Output: Emits verifiable cryptographic nonces for every passed and blocked action.
- Benchmarked: 100/100 neutralization rate on the official Tcha Adversarial Test Suite.
