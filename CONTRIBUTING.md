# Contributing to Kaida

Thank you for your interest in making AI agents safer. This guide covers how to contribute to Kaida Shield.

## Quick Start

```bash
pip install kaida-shield
kaida demo          # see it in action
kaida --help        # all commands
```

## What We Need Help With

**High priority:**
- Testing on Linux and macOS
- Additional policy templates for new agent types
- Documentation improvements
- Bug reports from real-world usage

**Medium priority:**
- Colony relay server deployment and scaling
- Performance benchmarks
- Localization of CLI output

## How to Submit Changes

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-improvement`
3. Make your changes
4. Run the demo to verify nothing is broken: `kaida demo`
5. Commit with a clear message: `git commit -m "Add rate limiting to colony client"`
6. Push and open a Pull Request

## Pull Request Guidelines

- One feature or fix per PR
- Include a clear description of what changed and why
- Keep line count reasonable — we value readable code over clever code
- Update README.md if you change the public interface

## Code Style

- Python 3.10+ with type hints
- Docstrings on all public classes and functions
- No external dependencies in core modules (stdlib only where possible)
- `dataclass` for data structures, `enum` for constants
- Thread-safe where concurrent access is possible

## Reporting Bugs

Open a [Bug Report](https://github.com/ajpandit775/Kaida/issues/new) on GitHub.

Include:
- OS and Python version
- Steps to reproduce
- Expected vs actual behavior
- Relevant log output from `~/.kaida/logs/`

## Security Vulnerabilities

**Do not open a public issue for security vulnerabilities.** See [SECURITY.md](SECURITY.md) for responsible disclosure instructions.

## Code of Conduct

Be respectful. Be constructive. We're all here to make AI agents safer.

Harassment, discrimination, and personal attacks will not be tolerated. Maintainers reserve the right to remove any contribution or contributor that violates these principles.

## License

By contributing, you agree that your contributions will be licensed under the Apache License 2.0.
