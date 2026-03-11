# Changelog

All notable changes to Kaida Shield will be documented in this file.

## [0.1.0] - 2026-03-04

### Added

- **8-layer security architecture** inspired by the human immune system
  - L1 Pre-Scanner: magic bytes, entropy analysis, archive bombs, phishing URLs
  - L2 Fuzzy Immunity: 15-dimensional feature vectors with cosine similarity
  - L3 Policy Engine: behavioral policies per task type (ALLOW/DENY/KILL/QUARANTINE)
  - L4 Sandboxed Cell: Docker container isolation (optional)
  - L5 Vision Cell: screenshot analysis for browser agents (optional, requires Playwright)
  - L6 Sensor: real-time syscall monitoring via eBPF or /proc fallback
  - L7 Quarantine: freeze-inspect-decide pipeline with forensic snapshots
  - L8 Colony Network: P2P threat sharing with HMAC-signed broadcasts
- **CLI commands**
  - `kaida scan file|url|cmd` — scan files, URLs, or commands for threats
  - `kaida demo` — 14 built-in scenarios demonstrating threat detection
  - `kaida shield run <command>` — run any command with behavioral policy monitoring
  - `kaida policies` — list all available security policy templates
  - `kaida setup` — interactive first-run configuration
- **Detection capabilities**
  - Executable detection (ELF, PE, Mach-O disguised as documents)
  - Zip bomb detection (compression ratio analysis)
  - High-entropy file detection (encrypted payloads)
  - Phishing URL detection (homograph attacks, suspicious TLDs, brand typosquatting)
  - Reverse shell detection (bash /dev/tcp, netcat, Python sockets)
  - Base64 obfuscation detection (encoded payloads piped to shell)
  - DNS tunneling detection (encoded subdomains)
  - Data exfiltration detection (POST with local file data)
  - Cryptocurrency miner detection (known tools and pool domains)
  - Credential harvesting URL detection (misspelled brands, login paths)
- **Policy engine** with 6 pre-built templates (code execution, web scraping, file analysis, API interaction, browser browsing, browser screenshot)
- **Fuzzy threat matching** — weighted cosine similarity catches mutated threats that hash-based systems miss
- **Colony gossip protocol** — reputation-based trust with hop-limited broadcast relay
- **147+ tests** across 7 modules with no external dependencies required
- **Zero hard dependencies** — works with Python stdlib alone; Docker, Playwright, eBPF are optional
- **Windows support** — ANSI color output, UTF-8 encoding, process monitoring all work on Windows

### Infrastructure

- Proper Python package structure (`kaida_shield/`)
- `pyproject.toml` with PEP 621 metadata
- CLI entry point via `pip install kaida-shield`
- Apache 2.0 license
- CI workflow (GitHub Actions)
- Contributing guide and security policy
