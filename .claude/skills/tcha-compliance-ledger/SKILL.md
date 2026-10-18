---
name: tcha-compliance-ledger
description: Immutable, cryptographic audit trail generator for Claude and autonomous agent tool actions. Builds Merkle tree logs with SHA-256 nonces for SOC 2 Type II and EU AI Act Article 15 compliance verification.
---

# Tcha Compliance Ledger

Provides automated, tamper-evident cryptographic logging for autonomous agents, ensuring that every tool execution, API fetch, and file modification has an indisputable audit record.

## Why This Matters

When autonomous agents operate inside enterprise environments, compliance auditors require:
1. **Proof of Action**: What tools did the agent invoke?
2. **Proof of Integrity**: Were logs altered after an incident?
3. **Proof of Boundary**: Did the agent exceed its defined security scope?

## How It Works

1. **Pre-Execution Hashing**: Intercepts tool calls and computes `SHA-256(timestamp + tool_name + arguments)`.
2. **Merkle Block Chaining**: Combines individual action hashes into a continuous Merkle tree ledger.
3. **Local or Cloud Storage**: Keeps records strictly on-premises in JSONL format, or syncs to enterprise Cloudflare KV / S3 storage if configured.

## Usage in Claude

Generate a compliance report for the current session:
```bash
npx tcha-protection ledger --export
# Verifies cryptographic integrity of past agent logs
npx tcha-protection ledger --verify
```

## Sample Audit Record

```json
{
  "sequence": 142,
  "timestamp": "2026-10-18T22:58:00Z",
  "tool": "filesystem.readFile",
  "status": "APPROVED",
  "policy_checked": "path_boundary",
  "nonce": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
  "merkle_root": "a89b3f02194c771da4bc234f9a0c128374d9e29a34bc9812df082736458923bc"
}
```
