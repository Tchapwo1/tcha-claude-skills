---
name: tcha-secret-shield
description: In-line credential and secret redaction guard for Claude. Intercepts sensitive strings (AWS access keys, OpenAI/Anthropic API tokens, database URIs, private keys, JWTs) before they are sent to LLM APIs, logged to terminals, or committed to git.
---

# Tcha Secret Shield

A deterministic, zero-latency credential sanitizer and redaction guard for Claude Code, Claude Desktop, and agentic workflows.

## Capabilities & Scopes

- **Zero-Exposure Interception**: Scans files, prompt inputs, and tool outputs before transmission.
- **Pattern Matching & Entropy Analysis**:
  - Cloud Providers: AWS (`AKIA...`), GCP Service Accounts, Azure Client Secrets.
  - LLM APIs: Anthropic (`sk-ant-...`), OpenAI (`sk-...`), Cohere, Mistral.
  - Infrastructure: Stripe secret keys (`sk_live_...`), GitHub PATs (`ghp_...`), npm tokens (`npm_...`).
  - Cryptographic Assets: PEM/RSA private keys, SSH keys (`id_rsa`, `id_ed25519`).
  - Database URIs: PostgreSQL, MySQL, Redis, MongoDB connection strings with embedded passwords.
- **Deterministic Token Replacement**: Replaces sensitive data with cryptographic placeholders (e.g. `[REDACTED_TCHA_AWS_SECRET_<HASH>]`) to preserve structural integrity without leaking secrets.

## When to Activate

Trigger this skill whenever:
1. Claude reads or displays local configuration files (`.env`, `credentials.json`, `config.yaml`, `id_rsa`).
2. An agent prepares a git commit or pushes code to an external repository.
3. Untrusted outputs are passed between multi-agent subtasks.

## Command Line Integration

Execute directly in Claude Code terminal:
```bash
npx tcha-protection sanitize --file .env
# Or pipe input through the sanitizer
cat config.json | npx tcha-protection sanitize
```

## Security Guarantees
- Operates 100% locally on your machine.
- Zero external network requests during redaction.
- Latency overhead: `<0.2ms`.
