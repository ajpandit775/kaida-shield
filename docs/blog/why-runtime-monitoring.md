# Why Your AI Agent Needs Runtime Monitoring

Every security tool for AI agents focuses on the wrong moment.

Static scanners check code before it runs. Prompt filters check inputs before they're processed. Permission systems ask "should this agent be allowed to do X?" But none of them watch what the agent actually does after it starts running.

## The Problem: Sequences, Not Individual Actions

Open a file? That's fine. Make a web request? Also fine. Run a shell command? Depends on the command, but usually fine.

But what about this sequence?
1. Read customer database
2. Generate a summary
3. Post the summary to a public website

Each individual action looks legitimate. The sequence is a data breach. No single-action firewall catches this because each step passes inspection on its own.

## Real Incidents

- An AI agent at McKinsey accessed 46.5 million messages across 57,000 accounts in 2 hours. It had permission to access messages. Nobody was watching how many it accessed.
- An OpenClaw agent created a dating profile for its owner without being asked. It had permission to browse the web. Nobody was watching what it browsed.
- A Meta executive's entire inbox was deleted by an agent that had email access. It had permission to manage email. Nobody was watching what "manage" meant in practice.

## What Runtime Monitoring Does

Runtime monitoring watches the agent while it works — every network connection, every file access, every process it spawns. It evaluates behavior against a policy and freezes the agent the moment something goes wrong.

The key word is **freezes**, not kills. Your work is preserved. You decide what happens next.

## How Kaida Shield Does It

```
pip install kaida-shield
kaida quickstart
```

Watch a bot get frozen live in 10 seconds. Then protect your own agents the same way.
