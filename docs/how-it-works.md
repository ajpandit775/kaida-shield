# How Kaida Shield Works

Kaida Shield protects AI agents using eight defense layers inspired by the human immune system. Each layer handles a different type of threat, and they work together to provide defense-in-depth — if one layer misses something, the next one catches it.

## The 8 Defense Layers

### Layer 1: Pre-Scanner

The first line of defense. Before your agent touches anything, the Pre-Scanner checks inputs for known danger signs:

- **File analysis** — identifies executables disguised as documents, checks for archive bombs (tiny files that expand to gigabytes), and flags files with unusually high randomness (a sign of encrypted payloads)
- **URL analysis** — detects phishing URLs using homograph attacks (replacing letters with look-alikes from other alphabets), brand impersonation, suspicious domain patterns, and insecure connections
- **Command analysis** — catches reverse shells, pipe-to-bash attacks, base64-obfuscated commands, DNS tunneling, data exfiltration, and cryptocurrency miner downloads

### Layer 2: Fuzzy Immunity

Traditional security tools match exact signatures — change one byte and they miss the threat. Kaida's Fuzzy Immunity system works differently.

Every threat is converted into a multi-dimensional feature profile. When a new input arrives, Kaida compares its profile against all known threats using similarity matching. This catches threats that have been slightly modified, repackaged, or mutated — the same way your immune system recognizes variants of a virus it's seen before.

### Layer 3: Policy Engine

The behavioral brain of Kaida. Policies define what "healthy behavior" looks like for each type of task. A web scraping bot should access the internet but not your local files. A file analysis bot should read files but not make network connections.

Policies are written in YAML and specify:
- **Allowed and denied actions** by category (file access, network, process spawning, etc.)
- **Resource limits** (CPU, memory, disk, network, execution time)
- **Anomaly detection thresholds** (data exfiltration ratios, burst activity detection, DNS query limits)
- **Default verdict** — what happens when an action isn't covered by any rule (defaults to DENY)

See [policy-format.md](policy-format.md) for the full YAML reference.

### Layer 4: Sandboxed Cell

For maximum isolation, Kaida can run your agent inside a container with:
- Read-only filesystem (the agent can't modify system files)
- All Linux capabilities dropped (no privilege escalation)
- Resource limits enforced at the kernel level
- Network restrictions based on the active policy

This layer is optional and requires Docker. Without Docker, Kaida still provides protection through the other seven layers.

### Layer 5: Vision Cell

For browser-based agents, Kaida can analyze what the agent sees on screen. This catches threats that text-based analysis misses:
- Fake login pages designed to steal credentials
- Visual impersonation of trusted brands
- Credential harvesting forms

This layer is optional and requires Playwright.

### Layer 6: Sensor

The Sensor monitors your agent's behavior in real time by observing system-level activity:
- File reads and writes
- Network connections
- Process spawning
- DNS queries

Every observed action is checked against the active policy. On Linux with root access, the Sensor uses eBPF for kernel-level visibility. On other systems, it falls back to process-level monitoring.

### Layer 7: Quarantine

When Kaida detects something suspicious, it doesn't just kill the process — it freezes it. The Quarantine system:

1. **Pauses** the agent instantly
2. **Takes a forensic snapshot** — what files were open, what network connections were active, what the agent was doing
3. **Scores the risk** based on all available evidence
4. **Decides** — auto-release if the risk is low, auto-kill if it's critical, or ask you to decide if it's ambiguous

This freeze-inspect-decide approach means fewer false positives and better evidence for understanding what happened.

### Layer 8: Colony Network

The Colony is an optional peer-to-peer threat intelligence network. When one Kaida node kills a threat, its signature is broadcast to every other node — like a vaccine spreading through a population.

Key properties:
- **Reputation-based trust** — nodes build trust over time; a new node's reports carry less weight than an established one's
- **Cryptographically signed** — broadcasts are signed so they can't be forged
- **Hop-limited** — broadcasts don't flood the network indefinitely

The Colony is opt-in. Kaida works fully standalone without it.

## How the Layers Work Together

Here's what happens when you run `kaida shield run python3 my_bot.py`:

1. **L1 Pre-Scanner** checks the command itself for danger patterns
2. **L3 Policy Engine** loads the appropriate behavioral policy
3. **L4 Sandboxed Cell** (if Docker is available) creates an isolated container
4. **L6 Sensor** starts monitoring the agent's system activity
5. As the agent runs, every action is checked against the policy
6. **L2 Fuzzy Immunity** compares any files or URLs the agent touches against known threats
7. If something triggers a rule, **L7 Quarantine** freezes the agent and evaluates the risk
8. If a threat is confirmed, **L8 Colony** broadcasts the signature to protect other nodes

The result: your agent runs normally when it behaves correctly, and gets caught immediately when it doesn't.

## Design Principles

- **Pessimistic by default** — anything not explicitly allowed is denied
- **No single point of failure** — eight independent layers, each catching different threat types
- **Graceful degradation** — Kaida works without Docker, without eBPF, without Playwright, without the Colony network. Each optional component adds protection but none are required
- **Zero hard dependencies** — the core runs on Python's standard library alone
