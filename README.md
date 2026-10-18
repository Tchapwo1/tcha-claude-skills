# 🛡️ Tcha Claude Security Suite
### The Deterministic Transport Firewall & Boundary Guard for Claude Code, Claude Desktop, & MCP

[![npm version](https://img.shields.io/npm/v/tcha-protection.svg?color=black&label=npm)](https://www.npmjs.com/package/tcha-protection)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Latency](https://img.shields.io/badge/Latency-%3C0.5ms-green.svg)](https://tcha.dev/report.html)
[![Neutralization](https://img.shields.io/badge/Adversarial%20Score-100%2F100-success.svg)](https://tcha.dev/report.html)
[![Protocol](https://img.shields.io/badge/Supports-Model%20Context%20Protocol-orange.svg)](https://modelcontextprotocol.io)

Autonomous agents don't have security perimeters. Once you give an agent access to execute terminal commands, modify files, and query MCP tools, **any untrusted input it reads becomes an attack vector**. 

Probabilistic system prompts fail against 70%+ of indirect prompt injections. **Tcha Claude Security Suite** fixes this deterministically by acting as an in-line, zero-latency transport firewall between Claude and your local environment.

---

## ⚡ 1-Minute Quick Start

### 1. Install Globally or Run via NPX
```bash
# Instant local audit (zero accounts, open-source MIT)
npx tcha-protection audit
```

### 2. Add to Claude Desktop
Add Tcha as a protective proxy in your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "tcha-guard": {
      "command": "npx",
      "args": ["-y", "tcha-protection", "guard"]
    }
  }
}
```

### 3. Add to Claude Code (.claude/skills)
Clone or copy the `.claude/skills` folder directly into your project root:

```bash
git clone https://github.com/Tchapwo1/tcha-claude-skills.git
cp -r tcha-claude-skills/.claude/skills ./your-project/.claude/
```

---

## 🧩 The 5 Core Security Skills

| Skill | Description | Attack Vector Neutralized |
| :--- | :--- | :--- |
| [`tcha-secret-shield`](.claude/skills/tcha-secret-shield/SKILL.md) | In-line redaction of API keys, `.env` files, and private tokens. | Accidental credential leakage to external LLM providers or git commits. |
| [`tcha-mcp-firewall`](.claude/skills/tcha-mcp-firewall/SKILL.md) | Boundary filter for Model Context Protocol tools and terminal commands. | Cloud Metadata SSRF (`169.254.169.254`), path traversal (`../../`), `rm -rf`. |
| [`tcha-injection-scanner`](.claude/skills/tcha-injection-scanner/SKILL.md) | Pre-execution scanner for scraped text, PDFs, and external web content. | Indirect prompt injections, zero-width steganography, and prompt delimiters. |
| [`tcha-audit-benchmark`](.claude/skills/tcha-audit-benchmark/SKILL.md) | On-demand adversarial penetration test running 100 automated probes. | Configuration oversights and unconfined tool privileges (`/audit-agent`). |
| [`tcha-compliance-ledger`](.claude/skills/tcha-compliance-ledger/SKILL.md) | Cryptographic Merkle tree audit logger with tamper-evident nonces. | Regulatory liability under **EU AI Act Article 15** & **SOC 2 CC6.1**. |

---

## 🔬 Benchmark & Neutralization Metrics

We evaluated Tcha against 100 adversarial test probes across 4 distinct threat classes:

| Threat Class | Probes | Neutralized | Escapes | Mean Overhead |
| :--- | :---: | :---: | :---: | :---: |
| **Cloud Metadata SSRF** (`169.254.169.254`) | 25 | **25 / 25** | 0 | 0.38 ms |
| **Path Traversal & Root Confinement** | 25 | **25 / 25** | 0 | 0.41 ms |
| **Destructive Command Execution** | 25 | **25 / 25** | 0 | 0.44 ms |
| **Indirect Delimiter Injection** | 25 | **25 / 25** | 0 | 0.49 ms |
| **Total Benchmark** | **100** | **100 / 100** | **0** | **0.43 ms** |

👉 **Read the full interactive benchmark report:** [https://tcha.dev/report.html](https://tcha.dev/report.html)

---

## 🏢 Architecture & Threat Model

```
┌─────────────────────────────────┐
│          Claude Agent           │
│   (Claude Desktop / Claude Code)│
└────────────────┬────────────────┘
                 │ Tool Invocation (e.g. bash, readFile, fetch)
                 ▼
┌────────────────────────────────────────────────────────┐
│           TCHA DETERMINISTIC TRANSPORT FIREWALL        │
│  ✓ Secret Redaction     ✓ SSRF & Cloud Metadata Block  │
│  ✓ Merkle Audit Nonce   ✓ Path Traversal Confinement   │
│  Latency: <0.5ms        Status: 100% Local / Zero Egress│
└────────────────┬───────────────────────────────────────┘
                 │ Sanitized & Verified Payload
                 ▼
┌─────────────────────────────────┐
│     Local Tools & MCP Servers   │
│ (Terminal, Filesystem, APIs)    │
└─────────────────────────────────┘
```

---

## 📜 Compliance Crosswalk

- **EU AI Act Article 15**: Demonstrable technical robustness, cyberattack resilience, and boundary enforcement.
- **SOC 2 Type II (CC6.1, CC6.6, CC6.8)**: Logical boundary restriction, data transmission protection, and tamper-evident audit logging.
- **OWASP Top 10 for LLMs**: Directly neutralizes LLM01 (Prompt Injection), LLM02 (Sensitive Information Disclosure), and LLM08 (Excessive Agency).

---

## 🤝 Community & Support

- **Official Web Hub**: [https://tcha.dev](https://tcha.dev)
- **NPM Package**: [`tcha-protection`](https://www.npmjs.com/package/tcha-protection)
- **Twitter / X**: [@tcha_dev](https://x.com/tcha_dev)
- **License**: [MIT](LICENSE) © 2026 Tcha Protection Pro
