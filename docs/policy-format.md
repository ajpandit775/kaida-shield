# Policy Format Reference

Kaida policies are YAML files that define what "healthy behavior" looks like for an AI agent task. The policy engine evaluates every observed action against these rules in real time.

## Basic Structure

```yaml
name: my_policy
description: What this policy is for
version: "1.0.0"
default_verdict: DENY

resource_limits:
  max_cpu_percent: 80.0
  max_memory_mb: 256
  max_disk_write_mb: 100
  max_net_egress_mb: 50
  max_open_files: 256
  max_child_processes: 4
  max_execution_seconds: 300

anomaly_detector:
  max_egress_ingress_ratio: 10.0
  idle_burst_threshold_seconds: 30.0
  burst_activity_count: 50
  max_dns_queries_per_minute: 30
  max_write_randomness: 7.5
  max_process_tree_depth: 3

rules:
  - category: net_connect
    pattern: ".*\\.example\\.com"
    verdict: ALLOW
    description: Allow connections to example.com
```

## Top-Level Fields

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `name` | string | Yes | — | Unique name for this policy |
| `description` | string | No | `""` | Human-readable description |
| `version` | string | No | `"1.0.0"` | Policy version for audit trail |
| `default_verdict` | string | No | `DENY` | What to do when no rule matches |
| `resource_limits` | object | No | See below | Hard resource ceilings |
| `anomaly_detector` | object | No | See below | Behavioral monitoring thresholds |
| `rules` | list | No | `[]` | Behavioral rules |

## Verdicts

Every rule and the default verdict use one of these values:

| Verdict | What Happens |
|---------|-------------|
| `ALLOW` | Action is permitted |
| `LOG` | Action is permitted but recorded for review |
| `DENY` | Action is silently blocked |
| `QUARANTINE` | Agent is frozen for inspection |
| `KILL` | Agent is terminated immediately |

## Resource Limits

Hard ceilings enforced by Kaida. The agent cannot exceed these regardless of its behavior.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `max_cpu_percent` | float | `80.0` | Maximum CPU usage (0-100) |
| `max_memory_mb` | int | `256` | Maximum RAM in megabytes |
| `max_disk_write_mb` | int | `100` | Maximum data written to disk |
| `max_net_egress_mb` | int | `50` | Maximum outbound network data |
| `max_open_files` | int | `256` | Maximum simultaneous open files |
| `max_child_processes` | int | `4` | Maximum spawned child processes |
| `max_execution_seconds` | int | `300` | Hard timeout (5 minutes default) |

## Anomaly Detector

Behavioral monitoring thresholds that catch unusual activity patterns.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `max_egress_ingress_ratio` | float | `10.0` | Flag if outbound data greatly exceeds inbound |
| `idle_burst_threshold_seconds` | float | `30.0` | How long idle before a sudden burst is suspicious |
| `burst_activity_count` | int | `50` | Activity-per-second threshold after idle |
| `max_dns_queries_per_minute` | int | `30` | Flag excessive DNS queries |
| `max_write_randomness` | float | `7.5` | Flag unusually random write patterns (max 8.0) |
| `max_process_tree_depth` | int | `3` | Max nested process spawning |

## Rules

Each rule matches a category of activity against a pattern.

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `category` | string | Yes | — | Type of activity (see categories below) |
| `pattern` | string | Yes | — | Pattern to match against the target |
| `verdict` | string | Yes | — | What to do when matched |
| `description` | string | Yes | — | Human-readable explanation |
| `max_count` | int | No | `null` | Rate limit: max occurrences per window |
| `rate_window_seconds` | float | No | `10.0` | Time window for rate limiting |

### Activity Categories

| Category | What It Matches |
|----------|----------------|
| `file_read` | Reading files (path is the target) |
| `file_write` | Writing files (path is the target) |
| `file_delete` | Deleting files (path is the target) |
| `net_connect` | Outbound network connections (host:port is the target) |
| `net_listen` | Opening a listening socket (port is the target) |
| `net_dns` | DNS lookups (domain is the target) |
| `process_spawn` | Spawning child processes (command is the target) |
| `process_exec` | Executing programs (binary path is the target) |
| `privilege_escalation` | Attempting privilege changes |
| `memory_map` | Memory mapping operations |
| `device_access` | Accessing hardware devices |

## Rule Evaluation Order

1. Rules are evaluated in the order they appear in the file
2. The **first matching rule** determines the verdict
3. If no rule matches, the `default_verdict` applies
4. Resource limits and anomaly detection run independently of rules

## Using a Custom Policy

```bash
kaida shield run --policy path/to/my_policy.yaml python3 my_bot.py
```

## Built-In Policy Templates

Kaida ships with these pre-built templates accessible by name:

- `code_execution` — general code running
- `web_scrape` — web scraping (optionally restricted to specific domains)
- `file_analysis` — file reading and processing
- `api_interaction` — API calls and data exchange
- `browser_browsing` — browser-based agents
- `browser_screenshot` — screenshot-only browser tasks

```bash
kaida shield run --policy web_scrape python3 my_scraper.py
kaida policies   # list all available templates
```

## Examples

See the [sample policies](../examples/sample_policies/) directory for complete, ready-to-use policy files.
