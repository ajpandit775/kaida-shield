# How Kaida Shield Works

Kaida Shield protects AI agents using multiple independent defense layers. Each layer handles a different type of threat, and they work together to provide defense-in-depth — if one layer misses something, the next one catches it.

## Protection Layers

### Input Scanning

The first line of defense. Before your agent touches anything, Kaida checks inputs for known danger signs:

- **File scanning** — identifies dangerous files disguised as safe ones, detects archive bombs, and flags suspicious payloads
- **URL scanning** — detects phishing URLs, brand impersonation, suspicious domain patterns, and insecure connections
- **Command scanning** — catches dangerous commands like reverse shells, unauthorized scripts, and obfuscated payloads

### Threat Matching

Traditional security tools match exact signatures — change one byte and they miss the threat. Kaida's threat matching works differently.

Every threat is converted into a profile. When a new input arrives, Kaida compares its profile against all known threats. This catches threats that have been slightly modified or repackaged — the same way your immune system recognizes variants of a virus it's seen before.

### Policy Enforcement

The behavioral brain of Kaida. Policies define what "healthy behavior" looks like for each type of task. A web scraping bot should access the internet but not your local files. A file analysis bot should read files but not make network connections.

Policies are written in YAML and specify:
- **Allowed and denied actions** by category (file access, network, process spawning, etc.)
- **Resource limits** (CPU, memory, disk, network, execution time)
- **Monitoring thresholds** (data transfer ratios, activity patterns, resource usage)
- **Default verdict** — what happens when an action isn't covered by any rule (defaults to DENY)

See [policy-format.md](policy-format.md) for the full YAML reference.

### Container Isolation

For maximum isolation, Kaida can run your agent inside a restricted container with limited permissions and resource controls. This layer is optional and requires Docker. Without Docker, Kaida still provides protection through all other layers.

### Visual Threat Detection

For browser-based agents, Kaida can analyze what the agent sees on screen. This catches threats that text-based analysis misses, like fake login pages designed to steal credentials. This layer is optional and requires Playwright.

### Behavioral Monitoring

Kaida monitors your agent's behavior in real time by observing system-level activity — file access, network connections, process spawning, and more. Every observed action is checked against the active policy.

### Quarantine

When Kaida detects something suspicious, it doesn't just terminate the process — it freezes it. The quarantine system pauses the agent, evaluates the risk based on all available evidence, and then decides: auto-release if the risk is low, auto-terminate if it's critical, or ask you to decide if it's ambiguous.

### Threat Intelligence Sharing

When one Kaida node stops a threat, that information can be shared with every other node — like a vaccine spreading through a population. Nodes build trust over time, and messages are cryptographically signed to prevent forgery. This layer is opt-in. Kaida works fully standalone without it.

## How the Layers Work Together

Here's what happens when you run `kaida shield run python3 my_bot.py`:

1. **Input scanning** checks the command for danger patterns
2. **Policy enforcement** loads the appropriate behavioral policy
3. **Container isolation** (if Docker is available) creates a restricted environment
4. **Behavioral monitoring** starts watching the agent's activity
5. As the agent runs, every action is checked against the policy
6. **Threat matching** compares any files or URLs the agent encounters against known threats
7. If something triggers a rule, **quarantine** freezes the agent and evaluates the risk
8. If a threat is confirmed, **threat intelligence** shares the information to protect other nodes

The result: your agent runs normally when it behaves correctly, and gets caught immediately when it doesn't.

## Design Principles

- **Pessimistic by default** — anything not explicitly allowed is denied
- **No single point of failure** — multiple independent layers, each catching different threat types
- **Graceful degradation** — Kaida works without Docker, without Playwright, without the threat network. Each optional component adds protection but none are required
- **Zero hard dependencies** — the core runs on Python's standard library alone
