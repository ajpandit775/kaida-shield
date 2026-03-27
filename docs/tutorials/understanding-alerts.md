# Understanding Kaida Alerts

When Kaida detects something, it shows one of three alert types. Here's what each means and what to do.

## 🔴 Known Threat (Red)

**What it means:** Your bot tried something that matches a known threat signature — phishing URL, reverse shell, crypto miner, etc.

**What to do:** This is almost always dangerous. Block it.

**Example:** Bot tried to connect to a known malware distribution site.

## 🟡 Policy Violation (Yellow)

**What it means:** Your bot accessed a website, file, or command that's not in your policy. This might be normal — you may have forgotten to include it.

**What to do:** Review the action. If it looks like normal bot behavior, click **Allow Always** to update your policy. If it looks suspicious, block it.

**Example:** Your email bot tried to access docs.google.com, but you only listed gmail.com in the policy.

## 🔵 Unusual Behavior (Blue)

**What it means:** Kaida detected an anomaly — your bot might be stuck in a loop, burning tokens, sending too many requests, or stalling.

**What to do:** Check if your bot is working correctly. Loops and token burn often mean the bot is confused or stuck.

**Example:** Your bot made 50 API calls in one minute when it normally makes 5.

## What "Frozen" Means

When Kaida freezes your bot, the process is paused — not killed. Your work is preserved. You can:
- **Allow** the action and resume
- **Block** the action and keep the bot frozen
- **Update rules** and restart
