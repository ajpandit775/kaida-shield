# Changelog

All notable changes to Kaida Shield will be documented in this file.

## [0.1.0] - 2026-03-04

### Added

- **Multi-layer security architecture** — defense-in-depth protection for AI agents
  - Input scanning — detects dangerous files, phishing URLs, and malicious commands before your agent runs
  - Threat matching — recognizes modified or repackaged versions of known threats
  - Behavioral policy enforcement — define what "safe behavior" looks like per task type
  - Container isolation (optional, requires Docker)
  - Visual threat detection for browser agents (optional, requires Playwright)
  - Real-time behavioral monitoring
  - Quarantine system — freeze, inspect, then decide
  - Threat intelligence sharing between Kaida nodes (optional)
- **CLI commands**
  - `kaida scan file|url|cmd` — scan files, URLs, or commands for threats
  - `kaida demo` — built-in scenarios demonstrating threat detection
  - `kaida shield run <command>` — run any command with behavioral policy monitoring
  - `kaida policies` — list all available security policy templates
  - `kaida setup` — interactive first-run configuration
  - `kaida ui` — open the visual dashboard
- **Detection capabilities**
  - Phishing URL detection (impersonation, suspicious domains, look-alike attacks)
  - Dangerous command detection (reverse shells, unauthorized scripts, obfuscated payloads)
  - Suspicious file detection (disguised executables, archive bombs, encrypted payloads)
  - Data exfiltration detection
  - Credential harvesting detection
- **Policy engine** with pre-built templates for common agent tasks
- **Threat intelligence network** — when one node detects a threat, all nodes are protected
- **Zero hard dependencies** — works with Python stdlib alone; Docker, Playwright are optional
- **Windows, macOS, and Linux support**

### Infrastructure

- Proper Python package structure (`kaida_shield/`)
- `pyproject.toml` with PEP 621 metadata
- CLI entry point via `pip install kaida-shield`
- Apache 2.0 license
- CI workflow (GitHub Actions)
- Contributing guide and security policy
