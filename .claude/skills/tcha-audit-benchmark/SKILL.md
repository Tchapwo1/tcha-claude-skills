---
name: tcha-audit-benchmark
description: On-demand security benchmark runner for Claude. Evaluates any repository, agent workspace, or MCP tool config against 100 adversarial attack probes across SSRF, path traversal, shell agency, and prompt injection.
---

# Tcha Audit Benchmark

Empowers Claude to run automated adversarial penetration audits against the current workspace, providing immediate vulnerability scoring, remediation guidance, and compliance readiness reports.

## Triggering the Audit

Developers can ask Claude:
- *"Audit our MCP server configuration for security vulnerabilities."*
- *"Run the Tcha 100-probe security test on this project."*
- *`/audit-agent`*

## Terminal Execution

Claude executes the zero-telemetry local audit:
```bash
npx tcha-protection audit
```

## Audit Output Structure

The benchmark evaluates:
1. **SSRF Resistance**: Tests metadata service queries (`169.254.169.254`, container loopbacks).
2. **Filesystem Confinement**: Checks boundary traversal, symlink escapes, and root file access.
3. **Execution Sandboxing**: Analyzes terminal capabilities and dangerous binary access.
4. **Credential Posture**: Scans environment variables and configuration files for exposed secrets.

### Compliance Crosswalk
Generates structured mapping against:
- **EU AI Act Article 15**: Technical robustness and cybersecurity.
- **SOC 2 Type II (CC6.1 - CC6.8)**: Logical access and boundary protection.
- **OWASP Top 10 for LLMs**: LLM01 (Prompt Injection) through LLM10 (Unbounded Consumption).

*Detailed interactive report available at [https://tcha.dev/report.html](https://tcha.dev/report.html).*
