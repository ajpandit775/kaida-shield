# Security Policy

## Reporting a Vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

Instead, please email **security@kaida.dev** with:

1. Description of the vulnerability
2. Steps to reproduce
3. Potential impact
4. Suggested fix (if you have one)

## Response Timeline

- **Acknowledgment:** Within 48 hours
- **Assessment:** Within 7 days
- **Fix (critical):** Within 14 days
- **Fix (non-critical):** Within 30 days

## Scope

The following are in scope for security reports:

- Sandbox escapes (container breakout, privilege escalation)
- Policy engine bypasses (circumventing behavioral rules)
- Colony protocol vulnerabilities (spoofed threat broadcasts, replay attacks)
- Authentication bypass in the REST API
- Denial of service against the sensor
- Information disclosure from quarantine forensic snapshots

## Out of Scope

- Vulnerabilities in Docker itself (report upstream)
- Social engineering attacks
- Issues requiring physical access to the host machine
- Denial of service via resource exhaustion (handled by policy limits)

## Recognition

We will credit security researchers in our release notes (unless you prefer to remain anonymous). We do not currently have a bug bounty program, but significant findings may be rewarded at our discretion.

## Supported Versions

| Version | Supported |
|---------|-----------|
| 0.1.x   | Yes       |
