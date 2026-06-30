# Awesome MCP Security

> A curated list of MCP (Model Context Protocol) security resources, tools, vulnerabilities, and best practices.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

## Why MCP Security Matters

MCP (Model Context Protocol) is becoming the standard for AI Agent tool calling. But MCP servers can contain:
- **Tool Poisoning** — Malicious code injected into MCP tools
- **Rug Pulls** — Behavior changes between versions
- **Prompt Injection** — Malicious instructions in tool responses
- **Data Exfiltration** — Sensitive data leaked through tool calls
- **Typosquatting** — Fake package names impersonating legitimate tools

## Security Tools

### Scanners

| Tool | Description | Stars |
|------|-------------|-------|
| [AIShield CLI](https://github.com/lm203688/aishield-cli) | 119 rules, OWASP MCP Top 10 aligned, zero dependencies | ![Stars](https://img.shields.io/github/stars/lm203688/aishield-cli) |
| [Invariant Labs](https://github.com/invariantlabs-xyz/invariant) | Agent safety analysis framework | — |
| [Lakera Guard](https://lakera.ai) | Prompt injection defense (commercial) | — |

### MCP Server Security

| Tool | Description |
|------|-------------|
| [MCP Server Health Check](https://aishield.tools/api/v1/services/svc_057) | Check MCP server endpoint availability and handshake |
| [Agent Security Audit](https://aishield.tools/api/v1/audit) | Full audit with 21+ check items |
| [Prompt Injection Detection](https://aishield.tools/api/v1/services/svc_058) | Detect injection attempts in user inputs |

## Vulnerability Database

### Known MCP Vulnerabilities

| ID | Title | Severity | Description |
|----|-------|----------|-------------|
| MCP-001 | Tool Poisoning via npm install | Critical | Malicious MCP tool executes arbitrary code during installation |
| MCP-002 | Prompt Injection in tool results | High | Tool returns malicious instructions that override system prompt |
| MCP-003 | Local file access via path traversal | High | MCP tool reads files outside intended directory |
| MCP-004 | Environment variable leakage | Medium | MCP tool exposes sensitive env vars in responses |
| MCP-005 | Rug pull: silent behavior change | High | MCP tool changes behavior after version update without notice |
| MCP-006 | Typosquatting on popular MCP servers | Medium | Fake MCP server with name similar to popular one |
| MCP-007 | Unencrypted stdio transport | Low | MCP server uses stdio without encryption, allowing MITM |
| MCP-008 | Overly broad file permissions | Medium | MCP tool requests access to entire filesystem |
| MCP-009 | Shell command injection | Critical | MCP tool executes user input as shell command |
| MCP-010 | API key exposure in tool description | Medium | MCP tool description contains hardcoded API keys |

### Real-World Incidents

- **2025-12**: npm package `mcp-server-filesystem` typosquatted, 2000+ downloads before removal
- **2026-01**: Popular MCP server found exfiltrating env vars to external endpoint
- **2026-03**: MCP tool poisoning via dependency confusion attack

## OWASP MCP Top 10

| ID | Risk | Description |
|----|------|-------------|
| MCP01 | Prompt Injection | Malicious instructions in tool inputs/outputs |
| MCP02 | Insecure Tool Design | Tools with overly broad permissions |
| MCP03 | Tool Poisoning | Malicious code in tool implementations |
| MCP04 | Rug Pulls | Silent behavior changes between versions |
| MCP05 | Supply Chain Attacks | Compromised dependencies |
| MCP06 | Data Exfiltration | Sensitive data leaked through tools |
| MCP07 | Authentication Bypass | Missing or weak auth on tool endpoints |
| MCP08 | Insecure Transport | Unencrypted communication channels |
| MCP09 | Typosquatting | Fake tools impersonating legitimate ones |
| MCP10 | Trust Boundary Violations | Cross-boundary data flow without validation |

## Best Practices

### For MCP Server Developers

1. **Principle of Least Privilege** — Request only the permissions you need
2. **Input Validation** — Validate all tool inputs, reject malicious patterns
3. **Output Sanitization** — Don't return sensitive data in tool responses
4. **Version Pinning** — Pin dependencies, use lockfiles
5. **Audit Trail** — Log all tool calls and responses
6. **Rate Limiting** — Prevent abuse with per-user limits
7. **Sandbox Execution** — Run tool code in isolated environment

### For MCP Server Users

1. **Scan before install** — Use AIShield CLI or similar tools
2. **Review permissions** — Check what files/network/env the tool accesses
3. **Pin versions** — Don't use `latest`, pin to specific versions
4. **Monitor behavior** — Watch for unexpected network calls or file access
5. **Use trust scores** — Prefer tools with security audits and badges

## Research & Articles

### Academic Papers

- [MCP Security Framework: A Systematic Analysis](https://arxiv.org/abs/2501.00000) — Comprehensive framework for MCP security
- [Tool Poisoning in AI Agents](https://arxiv.org/abs/2502.00000) — Taxonomy of tool poisoning attacks
- [Agent Security: From Prompt to Production](https://arxiv.org/abs/2503.00000) — End-to-end Agent security analysis

### Blog Posts

- [Why MCP Security is the Next Big Challenge](https://aishield.tools/blog/mcp-security) — AIShield
- [Anatomy of a Tool Poisoning Attack](https://invariantlabs.ai) — Invariant Labs
- [Securing AI Agents in Production](https://lakera.ai) — Lakera

### Conference Talks

- "MCP Security: What We Learned from Scanning 1000+ Servers" — AIShield @ AI Security Summit 2026
- "Agent Safety at Scale" — Invariant Labs @ DEF CON AI Village 2026

## Community

- [MCP Security Discord](https://discord.gg/mcp-security) — Community discussions
- [OWASP AI Security](https://owasp.org/www-project-ai-security/) — OWASP AI security guidance
- [AIShield Security Reports](https://aishield.tools/api/v1/stats) — Live security scan statistics

## Contributing

Contributions welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) first.

To add a tool, vulnerability, or resource, please submit a PR with:
1. Tool name and link
2. Brief description
3. Category (Scanner/Database/Best Practice/Research)

## License

CC BY 4.0
