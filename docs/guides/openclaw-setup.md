# Protecting OpenClaw Agents with Kaida Shield

OpenClaw gives your AI agent real power — file access, web browsing, shell commands, messaging. Kaida Shield makes sure it stays within bounds.

## Quick Setup

1. Install Kaida Shield:
   ```
   pip install kaida-shield
   ```

2. See it work in 10 seconds:
   ```
   kaida quickstart
   ```

3. Create a policy for your OpenClaw agent:
   ```
   kaida ui
   ```
   Go to the **Rules** tab and describe what your agent should do in plain English. For example:

   *"My OpenClaw agent manages my email, calendar, and can browse the web for research. It should not access social media, financial sites, or modify system files."*

4. Run OpenClaw through Kaida:
   ```
   kaida shield run openclaw
   ```

## What Kaida Monitors

When your OpenClaw agent runs through Kaida, every action is checked:
- **Network connections** — which websites does it contact?
- **File access** — which files does it read or write?
- **Process spawning** — does it launch other programs?
- **Resource usage** — is it consuming too much CPU/memory?
- **Behavioral patterns** — is it looping, burning tokens, or stalling?

## What Happens When Something Goes Wrong

If your agent tries to access a website not in your policy, Kaida **freezes** the process — it doesn't kill it. Your work is preserved. You get a notification (terminal, dashboard, Telegram, or email) and you decide:

- **Allow Once** — let this action through, keep monitoring
- **Allow Always** — add this to the policy permanently
- **Block** — kill the action and keep the agent frozen

## Tips for OpenClaw Users

- Start in **Supervised mode** for the first few runs. This way Kaida asks you before blocking anything.
- Your first run will likely trigger several freezes — that's normal. Your agent accesses things you didn't think to include in the policy.
- Use the **Activity** tab in the dashboard to see everything your agent did.
- After a few runs, switch to **Autonomous mode** once you trust the policy is complete.
