# Frequently Asked Questions

## General

### What is Kaida Shield?

Kaida Shield is a security runtime that wraps AI agents in layered protection. It monitors what your agent does — file access, network connections, process spawning — and blocks anything that violates the behavioral policy you define.

### Who is Kaida Shield for?

Anyone running AI agents that interact with their computer, files, or the internet. Whether you're a developer building autonomous agents or a non-technical user running a bot for the first time, Kaida adds a safety layer between the agent and your system.

### Does Kaida slow down my agent?

For most tasks, the overhead is negligible. Threat scanning adds a few milliseconds per input. Behavioral monitoring runs in the background without blocking normal execution.

### Does Kaida work on Windows?

Yes. Kaida Shield supports Windows, macOS, and Linux. Some advanced monitoring features are platform-specific, but Kaida automatically uses the best available method on each platform.

### Is Kaida Shield free?

Yes. Kaida Shield is open source under the Apache 2.0 license. It's free for personal and commercial use.

---

## Installation

### What Python version do I need?

Python 3.10 or newer.

### Does Kaida require Docker?

No. Docker enables container isolation for maximum protection, but all other protection layers work without it. Kaida automatically detects what's available and uses whatever protection it can.

### Can I install Kaida in a virtual environment?

Yes. `pip install kaida-shield` works in any virtual environment.

---

## Usage

### How do I scan a suspicious URL?

```bash
kaida scan url https://suspicious-site.com
```

Kaida returns **SAFE**, **SUSPICIOUS**, or **DANGEROUS** with details on what was detected.

### How do I protect my bot?

```bash
kaida shield run python3 my_bot.py
```

This runs your bot with Kaida monitoring every action against the default policy.

### How do I choose the right policy?

Use the built-in template that matches your agent's task:

- Running code? Use `code_execution` (default)
- Scraping websites? Use `web_scrape`
- Reading/processing files? Use `file_analysis`
- Calling APIs? Use `api_interaction`
- Browser automation? Use `browser_browsing`

```bash
kaida shield run --policy web_scrape python3 my_scraper.py
```

### Can I write my own policies?

Yes. Policies are YAML files that define allowed actions, resource limits, and monitoring thresholds. See [policy-format.md](policy-format.md) for the full reference.

### What happens when Kaida catches something?

It depends on the verdict in the matching rule:

- **DENY** — the action is silently blocked
- **QUARANTINE** — the agent is frozen while Kaida evaluates the risk
- **KILL** — the agent is terminated immediately

In quarantine mode, low-risk events may be auto-released, high-risk events auto-terminated, and ambiguous cases wait for your decision.

---

## Threat Intelligence

### What is the Colony?

The Colony is an optional network where Kaida nodes share threat intelligence. When one node detects and stops a threat, that information is shared with all other nodes to protect them too.

### Do I have to join the Colony?

No. The Colony is opt-in. Kaida works fully standalone without it.

### How do I disable the Colony?

```bash
export KAIDA_COLONY=off
```

### Is my data shared on the Colony?

No personal data is shared. Only threat signatures of confirmed threats are shared between nodes. Messages are cryptographically signed to prevent forgery.

---

## Security

### Can Kaida guarantee my agent is safe?

No security tool can guarantee complete protection. Kaida significantly reduces risk through multiple independent defense layers, but it's not a substitute for responsible AI usage, professional security auditing, or common sense.

### What if Kaida has a false positive?

If Kaida blocks something that should be allowed, you can:
1. Adjust your policy to allow the specific action
2. Adjust monitoring thresholds for your use case
3. Use `LOG` verdict instead of `DENY` to observe before blocking

### I found a security vulnerability. What do I do?

**Do not open a public issue.** Email security@kaida.dev with details. See [SECURITY.md](../SECURITY.md) for the full responsible disclosure policy.

---

## Troubleshooting

### `kaida: command not found`

Make sure the directory where pip installs scripts is in your PATH. Try:

```bash
python -m kaida_shield.shield --help
```

### `kaida demo` shows errors

Run `kaida setup` first to initialize the configuration directory. If the issue persists, check that you're running Python 3.10+:

```bash
python --version
```

### The dashboard won't open

`kaida ui` starts a local web server on port 8080. Make sure nothing else is using that port. You can change it:

```bash
kaida ui --port 9090
```
