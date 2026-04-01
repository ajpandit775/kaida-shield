# Changelog

All notable changes to Kaida Shield will be documented in this file.

## [0.3.8] - 2026-03-27

### Fixed
- **Accurate status reporting** — "COMPLETED WITH WARNINGS" when deny events exist (was incorrectly showing "COMPLETED SAFELY")
- **Tighter default policy** — code_execution now restricts network to package registries only
- **Reverse DNS** — network events show hostname instead of raw IP addresses
- **Expanded credential detection** — catches /etc/shadow, .ssh/*, .aws/*, .env, .pem, id_rsa, and more

---

## [0.3.7] - 2026-03-27

### Added
- **Runtime sensor integration** — monitoring loop now polls OS-level network connections, file access, and child processes in real time
- **--policy flag** — select policy templates from the command line: `kaida shield run --policy web_researcher python my_bot.py`
- **Policy aliases** — friendly names (email_assistant, web_researcher, etc.) map to built-in policies
- **Supervised mode** — pauses on violations and prompts Block / Allow Once / Allow Always

---

## [0.3.0] - 2026-03-15

### Added

- **Supervised mode** — Kaida now asks you before blocking, with Allow Once / Allow Always / Block options
- **Email notifications** — get alerts when your bot is frozen or killed (`kaida setup` to configure)
- **Telegram notifications** — real-time alerts with interactive approve/block buttons in Telegram (`kaida setup telegram`)
- **Allow Always learning** — approved actions are remembered so you're not asked twice
- **Setup wizard** — `kaida setup` walks you through email and Telegram configuration
- **Dashboard notification settings** — configure Email and Telegram from the UI
- 295 tests passing

---

## [0.2.1] - 2026-03-12

### Changed

- **Complete dashboard redesign** — 4 simple tabs instead of 7
- **Welcome wizard** for first-time users — guided setup with template picker
- **Browse button** to select bot files — no terminal commands needed
- **Amber violation alerts** with plain English explanations (not scary red)
- **Shield Strength meter** shows your protection level at a glance
- **Trust badge**: "100% Local — your data never leaves this computer"
- **Recent Bots dropdown** remembers your last 5 commands
- Policy builder now shows "Do this / Not this" examples

---

## [0.2.0] - 2026-03-12

### Added

- **Loop detection** — catches bots stuck repeating the same action and freezes them
- **Rate spike detection** — alerts on sudden activity bursts (configurable multiplier)
- **Stall detection** — notifies when bots go idle for too long
- **Token burn detection** — alerts on excessive outbound API calls
- **Resource anomaly detection** — catches sustained CPU/memory overuse
- **Configurable thresholds** — all anomaly detection settings tunable per policy in YAML
- 2 new demo scenarios (`kaida demo`) showing loop and rate spike detection
- Dashboard Status tab now shows "Anomaly Detection: Active"
- 182 tests passing

---

## [0.1.3] - 2026-03-11

### Added

- **Linux support** — Ubuntu, Debian, and other x86_64 Linux distributions
- **macOS support** — Apple Silicon (M1/M2/M3/M4) native builds
- **Automated multi-platform builds** — wheels built and published for all three platforms via CI
- **Cleaned up package metadata** — minimal, professional PyPI listing

### Fixed

- Build pipeline now works cross-platform (Linux, macOS, Windows)
- Wheel platform tags standardized for PyPI compatibility

---

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
