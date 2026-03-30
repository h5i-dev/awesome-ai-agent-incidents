# Contributing to Awesome AI Agent Incidents

Thank you for helping make this list more comprehensive and accurate.

## What belongs here

This list focuses specifically on **autonomous AI agent** security — incidents, vulnerabilities, attacks, and defenses that involve agents (systems with reasoning, memory, and tool use), not just standalone LLM chatbots.

Good additions include:

- **Real-world incidents** involving AI agents, MCP servers, or agentic workflows
- **CVEs** affecting AI agent frameworks, MCP infrastructure, or AI coding tools
- **Research papers** on attack techniques or defenses relevant to agentic systems
- **Open-source tools** for red teaming, guardrails, or monitoring of AI agents
- **Benchmarks** that measure agent security properties

## What does NOT belong here

- Incidents involving traditional software vulnerabilities with no AI-specific component
- Speculation or incidents without a verifiable source
- Promotional content without clear technical merit
- Duplicate entries (check before submitting)

## Format guidelines

### Incidents

```markdown
| Date | **Incident Name**: One-sentence description of what happened. | Impact summary | [Source Name](URL) |
```

- Use the format `Month YYYY` or `YYYY` if the month is uncertain
- Impact should be concrete: records stolen, organizations affected, dollar amount, etc.
- At least one source link is required; prefer primary sources (vendor disclosures, CVE entries, academic papers)

### CVEs

```markdown
| CVE-YYYY-NNNNN | Product / Component | CVSS score | One-sentence description |
```

### Research Papers

```markdown
| [Paper Title](URL) | Venue + Year | One-sentence TL;DR summarizing the key finding |
```

### Tools

```markdown
| [Tool Name](repo URL) | Maintainer | What it does and what threat it addresses |
```

## Process

1. Fork this repository
2. Add your entry in the appropriate section, maintaining alphabetical or chronological order within the section
3. Ensure your entry has a working URL
4. Submit a Pull Request with a brief description of what you are adding and why

## Accuracy

This is a security resource. Inaccurate incident descriptions can mislead practitioners. Please:

- Double-check dates, CVE numbers, and CVSS scores against primary sources
- If an incident's details are uncertain, note this explicitly (e.g., "reportedly", "est.")
- If you spot an error in an existing entry, please open an issue or submit a correction PR

## License

By contributing, you agree that your contributions will be released under the [MIT License](LICENSE).
