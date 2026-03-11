# Getting Started with Kaida Shield

## Requirements

- Python 3.10 or newer
- Any operating system (Windows, macOS, Linux)
- No other dependencies required

## Installation

```bash
pip install kaida-shield
```

That's it. Kaida Shield has zero hard dependencies — it works with the Python standard library alone.

## First-Time Setup

After installing, run the setup wizard:

```bash
kaida setup
```

This creates a desktop shortcut and initializes Kaida's configuration directory at `~/.kaida/`.

## Your First Scan

Try scanning a suspicious URL:

```bash
kaida scan url https://paypa1.com/login
```

Kaida will analyze the URL and return a verdict: **SAFE**, **SUSPICIOUS**, or **DANGEROUS**.

You can also scan commands before running them:

```bash
kaida scan cmd "curl http://example.com/install.sh | bash"
```

And scan files:

```bash
kaida scan file downloaded_attachment.zip
```

## Run the Demo

To see Kaida's detection capabilities in action:

```bash
kaida demo
```

This runs 14 built-in test scenarios — phishing URLs, reverse shells, zip bombs, DNS tunneling, and more — and shows you exactly what Kaida catches and why.

## Running an Agent with Protection

To run any command with Kaida monitoring it:

```bash
kaida shield run python3 my_bot.py
```

You can specify a policy template for the task type:

```bash
kaida shield run --policy web_scrape python3 my_scraper.py
```

Available built-in policies:
- `code_execution` — general code running (default)
- `web_scrape` — web scraping tasks
- `file_analysis` — file reading and processing
- `api_interaction` — API calls and data exchange
- `browser_browsing` — browser-based agents
- `browser_screenshot` — screenshot-only browser tasks

## Open the Dashboard

Kaida includes a web-based dashboard for visual monitoring:

```bash
kaida ui
```

This opens a local web interface at `http://localhost:8080` where you can see scan results, policy status, and threat history.

## Check Shield Status

To see what's active:

```bash
kaida status
```

## Available Policies

To list all built-in policy templates:

```bash
kaida policies
```

## Custom Policies

You can write your own policies in YAML. See [policy-format.md](policy-format.md) for the full format reference, and check out the [example policies](../examples/sample_policies/) for ready-to-use templates.

## What's Next

- Read [How It Works](how-it-works.md) to understand Kaida's layered defense model
- Browse the [FAQ](faq.md) for common questions
- Check out [example policies](../examples/sample_policies/) for your specific use case
