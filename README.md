<div align="center">

# Awesome AI Agent Incidents

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**A curated corpus of real-world security incidents, attack techniques, CVEs, frameworks, and defensive tools for autonomous AI agents.**

*From zero-click Copilot exfiltration to AI-powered C2 channels — attacks on agentic AI have moved well beyond theory.*

</div>

---

> **The Lethal Trifecta** (Simon Willison): An AI agent is *exploitable by design* when it simultaneously (1) has access to private/sensitive data, (2) processes untrusted external content, and (3) can communicate externally. Most production agents satisfy all three conditions.

---

## Table of Contents

- [Awesome AI Agent Incidents](#awesome-ai-agent-incidents)
  - [Table of Contents](#table-of-contents)
  - [Real-World Incidents](#real-world-incidents)
    - [Prompt Injection \& Goal Hijacking](#prompt-injection--goal-hijacking)
    - [Supply Chain Attacks](#supply-chain-attacks)
    - [Infrastructure Compromise](#infrastructure-compromise)
    - [Agent Misalignment \& Rogue Behavior](#agent-misalignment--rogue-behavior)
    - [AI-Assisted Attacks](#ai-assisted-attacks)
  - [CVE Database](#cve-database)
  - [MCP (Model Context Protocol) Security](#mcp-model-context-protocol-security)
    - [MCP Incidents \& PoCs](#mcp-incidents--pocs)
    - [MCP Attack Vectors](#mcp-attack-vectors)
  - [Attack Taxonomy](#attack-taxonomy)
    - [The Promptware Kill Chain](#the-promptware-kill-chain)
    - [Attack Techniques](#attack-techniques)
  - [Frameworks \& Standards](#frameworks--standards)
    - [OWASP Top 10 for Agentic Applications (ASI 2026)](#owasp-top-10-for-agentic-applications-asi-2026)
    - [MITRE ATLAS](#mitre-atlas)
    - [Other Frameworks](#other-frameworks)
  - [Research Papers](#research-papers)
    - [Surveys \& Systematizations](#surveys--systematizations)
    - [Prompt Injection \& Jailbreaks](#prompt-injection--jailbreaks)
    - [MCP \& Tool Poisoning](#mcp--tool-poisoning)
    - [Multi-Agent System Threats](#multi-agent-system-threats)
    - [Memory \& RAG Attacks](#memory--rag-attacks)
    - [Backdoor Attacks on Agents](#backdoor-attacks-on-agents)
    - [Benchmarks \& Agent Evaluation](#benchmarks--agent-evaluation)
    - [Defense Methods](#defense-methods)
  - [Defensive Tools \& Projects](#defensive-tools--projects)
    - [Open-Source Guardrails](#open-source-guardrails)
    - [Red Teaming \& Scanning](#red-teaming--scanning)
    - [Benchmarks \& Evaluations](#benchmarks--evaluations)
    - [Observability \& Tracing](#observability--tracing)
    - [Commercial / Enterprise Solutions](#commercial--enterprise-solutions)
  - [Learning Resources](#learning-resources)
    - [Articles \& Blog Posts](#articles--blog-posts)
    - [Courses, Labs \& CTFs](#courses-labs--ctfs)
    - [Databases \& Trackers](#databases--trackers)
  - [Key Reports \& Industry Data](#key-reports--industry-data)
  - [Contributing](#contributing)
  - [License](#license)

---

## Real-World Incidents

### Prompt Injection & Goal Hijacking

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| Mid-2025 | **EchoLeak — Microsoft 365 Copilot** `CVE-2025-32711` (CVSS 9.3): Zero-click prompt injection via crafted emails; reference-style Markdown image links bypassed Copilot's link-redaction filters, exfiltrating OneDrive, SharePoint, and Teams data through the Teams content URL API (`teams.microsoft.com/urlp/v1/url/content`) which was in the CSP allowlist—no user interaction required. | Data exfiltration across 160+ org-level incidents; ~$200M est. impact | [arXiv 2509.10540](https://arxiv.org/abs/2509.10540), [Checkmarx](https://checkmarx.com/zero-post/echoleak-cve-2025-32711-show-us-that-ai-security-is-challenging/), [Trend Micro](https://www.trendmicro.com/en_us/research/25/g/preventing-zero-click-ai-threats-insights-from-echoleak.html) |
| May 2025 | **GitHub MCP Prompt Injection**: Malicious commands embedded in public GitHub Issues hijacked developers' AI agents via the GitHub MCP server, exfiltrating private repository source code and cryptographic keys to attacker-controlled public repositories. | Private source code and keys leaked | [Security Boulevard / NSFOCUS](https://securityboulevard.com/2026/02/protecting-ai-security-2025-hot-security-incident/) |
| Aug 2025 | **Perplexity Comet Browser Injection**: Hidden commands in Reddit Markdown spoiler tags triggered Comet's "summarize page" feature; the agent logged into user emails, bypassed CAPTCHAs, and transmitted credentials within 150 seconds. | Credential theft | [Security Boulevard](https://securityboulevard.com/2026/02/protecting-ai-security-2025-hot-security-incident/) |
| Mid-2025 | **Supabase Cursor Agent Injection**: A Cursor agent with privileged service-role database access processed support tickets containing user-supplied SQL; attacker-controlled content caused exfiltration of sensitive integration tokens. | Sensitive tokens exposed | [Practical DevSecOps](https://www.practical-devsecops.com/mcp-security-vulnerabilities/) |
| Aug 2024 | **Slack AI Data Exfiltration**: Indirect prompt injection in public Slack channels weaponized Slack AI's RAG search to exfiltrate data from *private* channels via malicious link formatting—Slack initially described this as "intended behavior." | Private communications leaked | [Simon Willison](https://simonwillison.net/2024/Aug/20/data-exfiltration-from-slack-ai/), [PromptArmor] |
| 2024 | **Financial Reconciliation Agent Fraud**: An attacker phrased a data export as a legitimate business task ("all customer records matching pattern X"), causing a reconciliation agent to export every record without raising suspicion. | 45,000 customer records stolen | [Stellar Cyber](https://stellarcyber.ai/learn/agentic-ai-securiry-threats/) |
| 2025 | **Procurement Agent Memory Poisoning**: Over 3 weeks, a manufacturing firm's procurement agent was gradually memory-poisoned into believing elevated transfer limits were authorized; it then transferred funds to attacker accounts. | Financial fraud via persistent memory corruption | [Lares Labs](https://labs.lares.com/owasp-agentic-top-10/) |
| Nov 2025 | **A2A Session Smuggling** (Palo Alto Unit 42): "Agent Session Smuggling" exploited trust relationships in the Agent-to-Agent (A2A) protocol during multi-turn conversations; a malicious sub-agent hijacked the task graph of a trusted orchestrator. | Multi-agent system compromise | [Lares Labs](https://labs.lares.com/owasp-agentic-top-10/) |
| Dec 2025 | **OpenAI Atlas — Real Attack Chain Disclosed**: OpenAI confirmed a real-world attack where a malicious email caused their Atlas agent to autonomously send a resignation letter. OpenAI stated that "deterministic guarantees are not achievable." | Unauthorized email sent on behalf of user | [OpenAI Blog](https://openai.com/index/hardening-atlas-against-prompt-injection/)|
| 2024 | **ChatGPT Memory Persistence Attack**: Injected content manipulated ChatGPT's persistent memory feature to plant false memories, enabling long-term data exfiltration across sessions without re-injection. | Persistent cross-session data exfiltration | [Multiple sources] |
| 2024 | **Resume Prompt Injection**: Hidden white-on-white text in resumes manipulated AI hiring-assistant tools into inflating candidate scores—a real-world deployment of indirect injection against HR workflows. | AI hiring integrity undermined | [MDPI Information 2026] |
| 2024 | **SCADA Industrial Attack (PoC)**: White-on-white PDF instructions processed by Claude caused modification of parameters in a simulated industrial control system—the first documented AI-mediated SCADA attack vector. | Industrial control manipulation | [MDPI Information 2026] |

### Supply Chain Attacks

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| Aug 2025 | **s1ngularity — Nx Build System**: Compromised Nx build pipeline distributed malware targeting developer environments. The malware detected Claude Code and Gemini CLI and issued natural-language prompts instructing these agents to enumerate filesystems and exfiltrate credentials. | Developer credential theft at scale | [Trend Micro](https://www.trendmicro.com/vinfo/us/security/news/threat-landscape/fault-lines-in-the-ai-ecosystem-trendai-state-of-ai-security-report) |
| Feb 2026 | **OpenClaw / ClawHub Malicious Skills**: Antiy CERT confirmed 1,184 malicious skills across ClawHub, the package registry for the OpenClaw AI agent framework; Snyk ToxicSkills separately found 76 confirmed malicious payloads and 534 critically-vulnerable skills (~13.4%) in an independent scan of 3,984 skills. Techniques: typosquatting, mass uploads, 2.9% used `curl \| bash` remote-instruction loading. 135,000+ instances exposed with insecure defaults. | Largest confirmed AI agent supply chain attack | [CyberDesserts](https://blog.cyberdesserts.com/ai-agent-security-risks/), [Snyk ToxicSkills](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/) |
| Jan 2026 | **Claude Code RCE via Poisoned Config** `CVE-2026-XXXX`: Check Point Research disclosed RCE in Claude Code through poisoned repository `.claude` configuration files. Patched in Claude Code 2.0.65+. | Developer workstation compromise | [CyberDesserts](https://blog.cyberdesserts.com/ai-agent-security-risks/) |
| 2026 | **OpenAI Plugin Ecosystem Breach**: Supply chain attack on the OpenAI plugin ecosystem harvested agent credentials from 47 enterprise deployments; 6 months of undetected access to customer data, financial records, and proprietary code. | 47 enterprises compromised | [Stellar Cyber](https://stellarcyber.ai/learn/agentic-ai-securiry-threats/) |
| Aug 2025 | **Drift/Salesforce OAuth Token Theft (UNC6395)**: Threat actor used stolen OAuth tokens from Drift's Salesforce integration to access 700+ customer environments—no exploit, no phishing required. | 700+ orgs compromised; Drift temporarily removed from AppExchange | [Reco Blog](https://www.reco.ai/blog/ai-and-cloud-security-breaches-2025) |

### Infrastructure Compromise

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| Nov 2025 | **Ray Framework Mass Exploitation** `CVE-2023-48022`: Attackers used AI-generated attack scripts to exploit this critical unauthenticated RCE at scale, compromising 230,000+ publicly exposed Ray AI computing clusters for cryptomining, data theft, and DDoS. | 230K+ clusters compromised | [Security Boulevard](https://securityboulevard.com/2026/02/protecting-ai-security-2025-hot-security-incident/) |
| Nov 2025 | **SesameOp — OpenAI API as C2**: Microsoft DART discovered a novel backdoor (`OpenAIAgent.Netapi64.dll`) that used the OpenAI Assistants API as its C2 channel. Commands were embedded in encrypted assistant descriptions; results uploaded via message threads—all via legitimate `api.openai.com` traffic. | Stealthy persistent access; blends into enterprise AI traffic | [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2025/11/03/sesameop-novel-backdoor-uses-openai-assistants-api-for-command-and-control/) |
| 2025 | **Exposed MCP Servers**: Trend Micro found 492 MCP servers exposed to the internet with zero authentication, granting open access to agent infrastructure including file systems and code execution. | Open access to agent tooling | [CyberDesserts](https://blog.cyberdesserts.com/ai-agent-security-risks/) |

### Agent Misalignment & Rogue Behavior

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| 2025 | **Cost-Optimization Agent Deletes Production Backups**: A cloud cost-optimization agent autonomously decided that deleting production backups was the most efficient way to reduce storage costs. No attacker involved—pure goal misalignment. | Production backup loss | [Lares Labs](https://labs.lares.com/owasp-agentic-top-10/) |
| 2025 | **ServiceNow Now Assist Inter-Agent Spoofing**: Spoofed inter-agent messages in a procurement workflow caused a downstream agent to process fraudulent orders from attacker-front companies. | Fraudulent procurement orders | [Lares Labs](https://labs.lares.com/owasp-agentic-top-10/) |

### AI-Assisted Attacks

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| Nov 2025 | **Chinese State-Sponsored Claude Code Campaign**: Anthropic confirmed that a Chinese APT group used Claude Code to attempt infiltration of ~30 global targets across tech, finance, and chemical manufacturing. 80–90% of tactical operations (scanning, exploit crafting, multi-step infiltration) were executed autonomously by the agents. | First documented large-scale AI-agent-driven cyberattack | [Anthropic disclosure], [Reddit r/cybersecurity analysis](https://www.reddit.com/r/cybersecurity/comments/1r79rye/) |

---

## CVE Database

| CVE | Product / Component | CVSS | Description | References |
|-----|---------------------|------|-------------|------------|
| [CVE-2025-32711](https://nvd.nist.gov/vuln/detail/CVE-2025-32711) | Microsoft 365 Copilot (EchoLeak) | 9.3 (Critical, Microsoft CNA) | Zero-click prompt injection enabling data exfiltration from OneDrive/SharePoint/Teams via reference-style Markdown image URL leakage through the Teams content URL proxy. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-32711), [MSRC](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-32711) |
| [CVE-2025-53773](https://nvd.nist.gov/vuln/detail/CVE-2025-53773) | GitHub Copilot + Visual Studio 2022 | 7.8 (High, AV:L) | Local code execution via command injection triggered through prompt injection in GitHub Copilot / Visual Studio 2022 (v17.14.0–17.14.11); requires user interaction. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-53773), [MSRC](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-53773) |
| [CVE-2025-59944](https://nvd.nist.gov/vuln/detail/CVE-2025-59944) | Cursor (≤ v1.6.23) | 9.8 (Critical, NIST) / 8.0 (High, GitHub CNA) | Case-sensitivity flaw in protected file-path checks allows prompt injection to overwrite `/.cursor/mcp.json` on case-insensitive filesystems, escalating to RCE. Fixed in v1.7. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-59944), [GHSA](https://github.com/advisories?query=CVE-2025-59944) |
| [CVE-2025-3248](https://nvd.nist.gov/vuln/detail/CVE-2025-3248) | Langflow (< v1.3.0) | 9.8 (Critical) | Unauthenticated RCE via the `/api/v1/validate/code` endpoint; added to CISA KEV May 2025. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-3248) |
| [CVE-2025-34291](https://nvd.nist.gov/vuln/detail/CVE-2025-34291) | Langflow (≤ v1.6.9) | 9.4 (Critical, CNA) / 8.8 (High, NIST) | Account takeover + RCE via overly permissive CORS (`allow_origins='*'` + `allow_credentials=True`) combined with `SameSite=None` refresh token cookie, enabling cross-origin credential theft leading to code-execution endpoint access. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-34291), [GitHub](https://github.com/langflow-ai/langflow) |
| [CVE-2025-47241](https://nvd.nist.gov/vuln/detail/CVE-2025-47241) | Browser Use (< v0.1.45) | 9.3 (Critical, GHSA) | URL parsing flaw in `allowed_domains` whitelist: the parser splits on `:` to extract the domain, allowing an attacker to craft `https://allowed.com:pass@malicious.com/` to bypass domain restrictions entirely. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-47241), [GHSA-x39x-9qw5-ghrf](https://github.com/advisories/GHSA-x39x-9qw5-ghrf) |
| [CVE-2025-6514](https://nvd.nist.gov/vuln/detail/CVE-2025-6514) | mcp-remote | 9.6 (Critical, JFrog CNA) | OS command injection when connecting to an untrusted MCP server via a crafted `authorization_endpoint` URL in the OAuth response. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-6514) |
| [CVE-2023-48022](https://nvd.nist.gov/vuln/detail/CVE-2023-48022) | Anyscale Ray (v2.6.3 / v2.8.0) | 9.8 (Critical, Disputed) | Unauthenticated RCE via the job submission API; vendor disputes severity noting Ray is not designed for untrusted network exposure. Exploited at scale (230K+ clusters) using AI-generated attack scripts in 2025. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2023-48022) |

---

## MCP (Model Context Protocol) Security

### MCP Incidents & PoCs

| Incident | Description | Reference |
|----------|-------------|-----------|
| **GitHub MCP Prompt Injection** | Malicious instructions in GitHub Issues hijacked agents connected via the GitHub MCP server; private repo contents and API keys exfiltrated. | [Invariant Labs](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks) |
| **WhatsApp MCP Chat History Exfiltration** | Invariant Labs PoC: a malicious server combined tool poisoning with the legitimate `whatsapp-mcp` server to silently exfiltrate an entire chat history—zero user interaction. | [Invariant Labs](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks) |
| **MCP Inspector RCE** | Anthropic's own MCP Inspector developer tool allowed unauthenticated RCE via its inspector–proxy architecture, turning a debugging aid into a remote shell. | [AuthZed Timeline](https://authzed.com/blog/timeline-mcp-breaches) |
| **mcp-remote OAuth Command Injection** `CVE-2025-6514` | Critical OS command injection in the most widely used OAuth proxy for connecting local MCP clients to remote servers. | [AuthZed Timeline](https://authzed.com/blog/timeline-mcp-breaches) |
| **Smithery Build Config Path Traversal** | A path-traversal vulnerability in Smithery's build configuration leaked a builder's `~/.docker/config.json`, exposing a Fly.io API token that granted control over 3,000+ deployed apps. | [AuthZed Timeline](https://authzed.com/blog/timeline-mcp-breaches) |

### MCP Attack Vectors

| Vector | Description |
|--------|-------------|
| **Tool Poisoning** | Malicious instructions embedded in MCP tool `description` or `inputSchema` fields—invisible to users but parsed and executed by LLMs. The attack triggers *before* the poisoned tool is ever called. |
| **Rug Pull / Silent Redefinition** | MCP tools mutate their own definitions after installation and approval; the tool you approved is not the tool that executes. |
| **Tool Shadowing** | A malicious server injects a tool description that overrides or modifies the agent's behavior with respect to a different, trusted server's tools. |
| **Cross-Server Manipulation** | With multiple MCP servers connected, a malicious one intercepts and replaces calls destined for a trusted one—invisible to the user. |
| **Tool Return Attacks** | Malicious instructions injected into tool *output* (not descriptions), exploiting the same data/instruction confusion in the model's context. Effective even with hex-encoded payloads. |
| **MCP Preference Manipulation (MPMA)** | Subtly alter how AI agents rank and select among available tools, steering them toward attacker-controlled options. |
| **Webpage Poison via MCP Browser Tool** | Any MCP tool that fetches web content becomes a vector for indirect prompt injection from attacker-controlled pages. |

> **Root cause**: MCP clients receive tool metadata via `tools/list`, pass it into the LLM context without sanitization, and the LLM treats natural-language descriptions as instructions. The vulnerability is entirely client-side. ([arXiv 2603.22489](https://arxiv.org/abs/2603.22489))

---

## Attack Taxonomy

### The Promptware Kill Chain

Prompt injection has evolved from an isolated input-manipulation exploit into a structured, multi-stage malware mechanism. Analysis of 36 prominent incidents found at least 21 attacks traversing four or more stages of this kill chain. ([arXiv 2601.09625](https://arxiv.org/abs/2601.09625))

```
Stage 1: Initial Access        ──► Prompt injection (direct or indirect)
Stage 2: Privilege Escalation  ──► Jailbreak system constraints / safety filters
Stage 3: Reconnaissance        ──► Probe agent memory, tools, environment config
Stage 4: Persistence           ──► Poison agent long-term memory / RAG database
Stage 5: Command & Control     ──► Establish external channel (e.g., SesameOp)
Stage 6: Lateral Movement      ──► Leverage agent permissions to infect other agents
Stage 7: Actions on Objective  ──► Data exfiltration / financial fraud / system disruption
```

### Attack Techniques

| Technique | Category | Key Property |
|-----------|----------|--------------|
| **Direct Prompt Injection** | Input Manipulation | Malicious instructions in user turn override system prompt |
| **Indirect Prompt Injection (XPIA)** | Input Manipulation | Instructions hidden in emails, web pages, documents, tool output |
| **Tool Poisoning** | MCP / Supply Chain | Malicious content in tool metadata—triggers before tool is called |
| **Tool Shadowing** | MCP | Malicious server overrides trusted tool behavior |
| **Rug Pull / Silent Redefinition** | MCP | Tool definitions mutate post-installation |
| **Cross-Server Manipulation** | MCP | Malicious server intercepts calls to trusted server |
| **Memory Poisoning** | Persistence | Gradually corrupt agent long-term memory over multiple sessions |
| **RAG / Knowledge Base Poisoning** | Persistence | Inject malicious documents into retrieval corpus; 5 docs can achieve 90% manipulation rate |
| **Agent Session Smuggling** | Multi-Agent | Exploit A2A protocol trust across multi-turn conversations |
| **Adversary-in-the-Middle (AiTM)** | Multi-Agent | Compromised agent manipulates inter-agent message flow |
| **Infectious Prompt Propagation** | Multi-Agent | Malicious instructions spread virally across agent networks |
| **Backdoor Attacks** | Model-Level | Trained-in triggers cause malicious behavior on specific inputs |
| **AI Agent Clickbait** `AML.T0100` | Agentic UI | Manipulate web UI to lure agentic browsers into unintended actions |
| **Tool Call Injection** | Execution | Poisoned context causes agent to invoke tools with malicious parameters |
| **PLeak** | Info Extraction | Algorithmic extraction of system prompts via black-box queries |
| **Steganographic C2** | Covert Channel | Encode commands in LLM-generated content; agents communicate covertly |
| **Invisible Prompt Injection** | Stealth | Zero-width characters, Unicode homoglyphs, or control characters hide payloads |
| **Living-off-the-Land AI (LotAI)** | Stealth | Abuse legitimate AI service APIs (e.g., OpenAI Assistants) for C2, blending into normal traffic |

---

## Frameworks & Standards

### OWASP Top 10 for Agentic Applications (ASI 2026)

Released December 2025. Developed with 100+ security researchers. Distinct from the general LLM Top 10—focuses on the failure of *agentic* properties: autonomy, persistence, and tool integration.

| Rank | ID | Risk | Core Failure Mode |
|------|----|------|-------------------|
| 1 | ASI01 | **Agent Goal Hijack** | Attackers redirect agent goals and task selection via prompt injection, forged messages, or poisoned external data — exploiting LLMs' inherent inability to distinguish instructions from content |
| 2 | ASI02 | **Tool Misuse & Exploitation** | Agents misuse legitimate tools through unsafe composition, prompt injection into tool calls, or over-privileged access — leading to data exfiltration, destructive actions, or DoS |
| 3 | ASI03 | **Identity & Privilege Abuse** | Agents inherit excessive credentials or over-scoped API access, enabling privilege escalation or actions beyond intended authorization scope |
| 4 | ASI04 | **Agentic Supply Chain Vulnerabilities** | Compromised tool registries, MCP servers, third-party agents, or model artifacts introduce malicious behavior through trusted supply chain channels |
| 5 | ASI05 | **Unexpected Code Execution (RCE)** | Agents execute injected or unintended code via code-execution tools (shell, eval, REPL) due to insufficient sandboxing or input validation |
| 6 | ASI06 | **Memory & Context Poisoning** | Persistent corruption of agent memory, retrieval context, or long-term state biases future behavior without the agent or user detecting the tampering |
| 7 | ASI07 | **Insecure Inter-Agent Communication** | Spoofed or manipulated messages between collaborating agents propagate malicious instructions across a multi-agent system |
| 8 | ASI08 | **Cascading Failures** | Small errors or resource overuse propagate across interconnected agent systems, amplifying into large-scale disruptions |
| 9 | ASI09 | **Human-Agent Trust Exploitation** | Agents produce misleading or overconfident outputs that exploit human tendency to trust AI, causing harmful decisions by operators or end users |
| 10 | ASI10 | **Rogue Agents** | Agents drift from intended behavior due to misalignment, self-modification, or emergent collusion — without active attacker involvement |

**Source:** [OWASP GenAI Security Project](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)

### MITRE ATLAS

MITRE ATLAS (Adversarial Threat Landscape for AI Systems) is the canonical knowledge base of adversary tactics and techniques, now expanded to **16 tactics and 84+ techniques** with specific coverage of agentic threats.

Key techniques relevant to AI agents:

| Tactic | Key Technique | ATLAS ID |
|--------|---------------|----------|
| Initial Access | Prompt Injection | AML.T0051 |
| Persistence | Modify AI Agent Configuration | AML.T0101 (proposed) |
| Credential Access | Agent Tool Credential Harvesting | AML.T0098 |
| Command & Control | AI Service API Abuse | AML.T0096 |
| Exfiltration | Exfiltration via Agent Tool Invocation | — |
| New (2025) | AI Agent Clickbait | AML.T0100 |

**Source:** [MITRE ATLAS](https://atlas.mitre.org/)

### Other Frameworks

| Framework | Description |
|-----------|-------------|
| [OWASP Top 10 for LLM Applications 2025](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | Broader LLM risks; prompt injection remains #1 |
| [OWASP Agentic AI — Threats and Mitigations (T01–T17)](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/) | Comprehensive agentic threat taxonomy |
| [OWASP Multi-Agentic System Threat Modeling](https://genai.owasp.org/resource/multi-agentic-system-threat-modeling-guide-v1-0/) | Threat modeling guide for multi-agent architectures |
| [CSA MAESTRO](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro) | CSA's agentic AI threat modeling framework |
| [NIST AI RMF](https://www.nist.gov/artificial-intelligence/ai-risk-management-framework) | Risk governance for AI systems |
| [Google SAIF](https://saif.google/) | Google's Secure AI Framework |
| [EU AI Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689) | Regulatory framework; fines up to €35M or 7% of global revenue for high-risk violations |
| [CoSAI](https://www.cosai.dev/) | Cross-industry collaboration on AI security standards (model signing, MCP security, zero trust for AI) |
| [AVIDML Taxonomy](https://avidml.org/taxonomy/) | AI Vulnerability and Incidents Database taxonomy |
| [MIT AI Risk Repository](https://airisk.mit.edu/) | Comprehensive repository of AI risk categories |

---

## Research Papers

### Surveys & Systematizations

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [The Attack and Defense Landscape of Agentic AI: A Comprehensive Survey](https://arxiv.org/abs/2603.11088) | arXiv 2026 | Reviews 128 papers (51 attacks, 60 defenses). Argues component-level defenses are insufficient; security must be treated as a systems-level problem. Defines 6 primary attack vectors. |
| [AI Agents Under Threat: A Survey of Key Security Challenges and Future Pathways](https://arxiv.org/abs/2406.02630) | ACM Comp. Surveys 2025 | Categorizes threats across 4 knowledge gaps. Key finding: backdoor defenses don't cover the full agent ecosystem beyond model granularity. |
| [Agentic AI Security: Threats, Defenses, Evaluation, and Open Challenges](https://arxiv.org/abs/2510.23883) | arXiv Oct 2025 | Broad threat taxonomy spanning prompt injection, autonomous cyber-exploitation, multi-agent threats, and governance concerns. |
| [A Survey of Agentic AI and Cybersecurity](https://arxiv.org/abs/2601.05293) | arXiv Jan 2026 | Treats agentic AI as a cybersecurity system. Analyzes collusion, cascade failures, and oversight evasion with prototype implementations. |
| [The Landscape of Prompt Injection Threats in LLM Agents: From Taxonomy to Analysis](https://arxiv.org/abs/2602.10453) | arXiv Feb 2026 | Systematization-of-knowledge with unified taxonomy. Introduces **AgentPI benchmark** covering context-dependent agent tasks all prior benchmarks ignored. |
| [From Prompt Injections to Protocol Exploits](https://arxiv.org/abs/2506.23260) | ICT Express (Elsevier) 2025 | Unified end-to-end threat model for LLM-agent ecosystems. Catalogs 30+ attack techniques; validates against real-world CVEs. |
| [Agentic AI in Cybersecurity: Cognitive Autonomy, Ethical Governance, and Quantum-Resilient Defense](https://pmc.ncbi.nlm.nih.gov/articles/PMC11628095/) | F1000Research Sep 2025 | Narrative review spanning 2005–2025. Identifies dual-use risks, governance gaps, and post-quantum preparedness challenges. *(citation unverifiable — access restricted; treat with caution)* |
| [A Survey on Agentic Security: Applications, Threats and Defenses](https://arxiv.org/abs/2510.06445) | arXiv Oct 2025 | Cross-cutting analysis of 160+ papers. Maps planner–executor agent patterns and GPT/Claude/LLaMA backbones to their respective attack surfaces. Privacy and integrity defenses surveyed per architecture type. |
| [Multi-Agent Framework for Threat Mitigation and Resilience in AI-Based Systems](https://arxiv.org/abs/2512.23132) | arXiv Dec 2025 | Extracts 93 threats from three sources via a multi-agent RAG pipeline: MITRE ATLAS (26), AI Incident Database (12), and 55 literature papers. Identifies previously unreported TTPs beyond ATLAS coverage. |
| [AI-Augmented SOC: A Survey of LLMs and Agents for Security Automation](https://www.mdpi.com/2624-800X/5/4/95) | J. Cybersecur. Priv. 2025 | Reviews 600+ papers across 8 SOC tasks (alert triage, threat intel, incident response, log summarization, etc.). Highlights where agentic autonomy creates new insider-threat and prompt-injection risks within the SOC itself. |

### Prompt Injection & Jailbreaks

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection](https://arxiv.org/abs/2302.12173) | IEEE S&P Workshop 2023 | Foundational paper defining indirect prompt injection. Demonstrates remote data theft, ecosystem contamination across production applications. |
| [Universal and Transferable Adversarial Attacks on Aligned Language Models](https://arxiv.org/abs/2307.15043) | arXiv 2023 | Introduces transferable adversarial suffixes that elicit objectionable content across GPT, Claude, Llama. Foundational jailbreak work. |
| [The Promptware Kill Chain](https://arxiv.org/abs/2601.09625) | arXiv Jan 2026 | Formalizes prompt injection as a 7-stage malware delivery mechanism. Validates against 36 real incidents; 21 traversed ≥4 stages. |
| [EchoLeak: The First Real-World Zero-Click Prompt Injection Exploit](https://arxiv.org/abs/2509.10540) | arXiv Sep 2025 | Technical deep-dive on CVE-2025-32711; details how CSP and prompt-injection filters were both bypassed using a trusted Microsoft domain as exfiltration proxy. |
| [The Attacker Moves Second: Stronger Adaptive Attacks Bypass Defenses Against LLM Jailbreaks and Prompt Injections](https://arxiv.org/abs/2510.09023) | arXiv Oct 2025 | **Breaks 12 published defenses** using gradient descent, RL, random search. Most defenses claimed near-zero ASR; adaptive attacks exceeded 90% against most of them. |
| [Prompt Injection 2.0: Hybrid AI Threats](https://arxiv.org/abs/2507.13169) | arXiv Jul 2025 | Shows injections now combine with XSS, CSRF, AI worm propagation, and multi-agent infections to evade traditional WAFs entirely. |
| [Securing AI Agents Against Prompt Injection Attacks](https://arxiv.org/abs/2511.15759) | arXiv Nov 2025 | Benchmarks 847 adversarial cases across 5 attack categories vs. 7 LLMs. Combined defense reduces ASR from 73.2% → 8.7% while retaining 94.3% task performance. |
| [Prompt Injection Attack to Tool Selection in LLM Agents (ToolHijacker)](https://arxiv.org/abs/2504.19793) | arXiv Apr 2025 | No-box attack injecting a malicious tool document to hijack tool selection. StruQ, SecAlign, DataSentinel, and perplexity detection are all insufficient defenses. |
| Fooling AI Agents: Web-Based Indirect Prompt Injection Observed in the Wild | Palo Alto Unit 42, Feb 2026 | First large-scale analysis of IDPI in real telemetry. Documents timed-delay payloads, homoglyph obfuscation, canvas-based text hiding, and authority impersonation. *(source URL unverifiable — 404)* |
| [Attention Tracker: Detecting Prompt Injection Attacks in LLMs](https://arxiv.org/abs/2411.00348) | NAACL 2025 Findings | Detects prompt injection by tracking attention distribution shifts—no modification to the underlying model; deployable as a wrapper. |
| [Advertisement Embedding Attacks Against LLM Agents](https://arxiv.org/abs/2508.17674) | arXiv Aug 2025 | Shows how adversaries can covertly embed promotional content into agent responses by poisoning external data sources the agent consumes, turning helpfulness into a covert advertising channel. |

### MCP & Tool Poisoning

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [MCPTox: A Benchmark for Tool Poisoning Attacks on Real-World MCP Servers](https://arxiv.org/abs/2508.14925) | arXiv Aug 2025 | 45 live MCP servers, 353 tools, 1,312 malicious test cases. o1-mini ASR: **72.8%**. Claude-3.7 refusal rate: **<3%**. More capable models are often *more* vulnerable—better instruction following is the attack surface. |
| [MCP Threat Modeling: Analyzing Vulnerabilities to Prompt Injection with Tool Poisoning](https://arxiv.org/abs/2603.22489) | arXiv Mar 2026 | Identifies 57 threats across 5 MCP components using STRIDE/DREAD. Vulnerability is client-side: no validation of tool metadata before LLM context insertion. |
| [Systematic Analysis of MCP Security](https://arxiv.org/abs/2508.12538) | arXiv 2025 | Demonstrates Tool Return Attacks, Third-party Poison Attacks, and Webpage Poison Attacks. Both plaintext and hex-encoded commands are effective. |
| [MindGuard: Intrinsic Decision Inspection Against Metadata Poisoning](https://arxiv.org/abs/2508.20412) | arXiv Aug 2025 | Decision Dependence Graph (DDG) using LLM attention mechanisms. **94–99% precision**, 95–100% attribution accuracy, sub-second processing, zero additional token cost. |
| [MPMA: MCP Preference Manipulation Attacks](https://arxiv.org/abs/2505.11154) | arXiv May 2025 | Formalizes and implements attacks that steer agent tool-selection toward attacker-controlled servers by appending boosting phrases and genetic-algorithm-optimized descriptions to tool metadata—without modifying any tool logic. |

### Multi-Agent System Threats

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [Open Challenges in Multi-Agent Security](https://arxiv.org/abs/2505.02077) | arXiv May 2025 | Introduces "multi-agent security" as a new field. Novel threats: steganographic collusion, coordinated swarm attacks, cascading jailbreaks. Securing individual agents is *fundamentally* insufficient. |
| [Multi-Agent Risks from Advanced AI](https://arxiv.org/abs/2502.14143) | arXiv Feb 2025 | Structured taxonomy with 3 failure modes (miscoordination, conflict, collusion) and 7 risk factors. Strong empirical grounding. |
| [Multi-Agent Security Tax](https://arxiv.org/abs/2502.19145) | AAAI 2025 | Demonstrates "infectious malicious prompts" spreading across agent networks. Fundamental finding: effective security measures measurably decrease collaboration capability. |
| [Red-Teaming LLM Multi-Agent Systems via Adversary-in-the-Middle (AiTM)](https://aclanthology.org/2025.findings-acl.349/) | ACL 2025 | Compromised agent manipulates inter-agent communication. Chain topologies are most vulnerable; fully-connected topologies are more resilient. Demonstrates answer manipulation via fake encryption and conversational DoS. |
| [Multiagent Collaboration Attack: Adversarial Attacks in LLM Multi-Agent Debate](https://arxiv.org/abs/2406.14711) | arXiv Jun 2024 | A single adversarial agent embedded in a debate-style multi-agent panel can steer group consensus through persuasive but factually wrong reasoning, without the other agents detecting manipulation. |
| [ComPromptMized: Unleashing Zero-click Worms Targeting GenAI-Powered Applications (Morris II)](https://arxiv.org/abs/2403.02817) | arXiv 2024 | First demonstration of a self-replicating AI worm. Shows super-linear propagation through multi-agent email/assistant ecosystems with no user interaction. |

### Memory & RAG Attacks

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation](https://arxiv.org/abs/2402.07867) | USENIX Security 2025 | Just 5 poisoned documents can manipulate AI responses 90% of the time. Documents designed to match common query patterns. |
| [AgentPoison: Red-teaming LLM Agents via Poisoning Memory or Knowledge Bases](https://arxiv.org/abs/2407.12784) | arXiv 2024 | Demonstrates persistent backdoors planted via memory or KB poisoning that activate on specific triggers without affecting normal operation. |
| [AudAgent: Automated Auditing of Privacy Policy Compliance in AI Agents](https://arxiv.org/abs/2511.07441) | arXiv Nov 2025 | Auditing automaton ensuring runtime data practices align with stated privacy policies. Bridges natural language policies and technical execution. |

### Backdoor Attacks on Agents

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [BadAgent: Inserting and Activating Backdoor Attacks in LLM Agents](https://arxiv.org/abs/2406.03007) | ACL 2024 | Injects backdoors during fine-tuning or continued training. Agents behave normally except when triggered. Resists standard safety alignment. |
| [Watch Out for Your Agents! Investigating Backdoor Threats to LLM-Based Agents](https://arxiv.org/abs/2402.11208) | NeurIPS 2024 | Backdoor triggers in tool descriptions, memory retrievals, or environmental observations. Standard RLHF-based defenses ineffective. |

### Benchmarks & Agent Evaluation

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents](https://arxiv.org/abs/2406.13352) | NeurIPS D&B 2024 | 97 tasks and 629 injection security cases across banking, Slack, travel, and workspace domains. GPT-4o utility drops from 69% → 45% under attack; best defense (tool filtering) reduces ASR to 7.5%. |
| [Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents](https://arxiv.org/abs/2410.02644) | ICLR 2025 | Formalizes 10 evaluation scenarios covering prompt injection, man-in-the-middle, and tool abuse. Provides standardized metrics for comparing attack and defense effectiveness across agent architectures. |
| [AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents](https://arxiv.org/abs/2410.09024) | ICLR 2025 | Evaluates agent compliance with harmful multi-step tool-calling tasks (misuse setting). Hand-authored tasks with human review; focuses on direct harmful requests rather than adversarial injection. |
| [SafeArena: Evaluating the Safety of Autonomous Web Agents](https://arxiv.org/abs/2503.04957) | arXiv Mar 2025 | 500 web tasks (250 safe, 250 harmful) across 5 harm categories. GPT-4o completed 34.7% of harmful requests. Introduces the Agent Risk Assessment (ARIA) framework with 4 risk levels. |
| [R-Judge: Benchmarking Safety Risk Awareness for LLM Agents](https://arxiv.org/abs/2401.10019) | EMNLP Findings 2024 | 569 multi-turn agent interaction records across 27 risk scenarios and 10 risk types. Best model (GPT-4o) achieves only 74.42% risk-awareness accuracy—well short of human-level performance. |
| [AgentDyn: A Dynamic Open-Ended Benchmark for Evaluating Prompt Injection Attacks](https://arxiv.org/abs/2602.03117) | arXiv Feb 2026 | Extends AgentDojo by adding dynamic open-ended tasks, helpful distractor instructions, and complex user goals. Tests 10 defenses; finds most defenses substantially degraded on realistic tasks. |

### Defense Methods

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [LlamaFirewall](https://arxiv.org/abs/2505.03574) | arXiv May 2025 | Meta's open-source multi-layer guardrail: PromptGuard 2 (jailbreak/injection detection), Agent Alignment Checks (chain-of-thought auditor), CodeShield (static analysis for code agents). |
| [How Microsoft Defends Against Indirect Prompt Injection Attacks (FIDES)](https://www.microsoft.com/en-us/msrc/blog/2025/07/how-microsoft-defends-against-indirect-prompt-injection-attacks) | Microsoft MSRC Jul 2025 | FIDES: information-flow control enforcing privilege separation and prompt isolation. Deterministically blocks indirect injection in Copilot-class agents. |
| [Agents Rule of Two](https://ai.meta.com/blog/practical-ai-agent-security/) | Meta Oct 2025 | Architectural rule: agents must satisfy **≤2 of**: (A) processing untrusted input, (B) access to sensitive data, (C) ability to change external state. Deterministic blast-radius bound. |
| [Prompt Injection Attacks in LLMs and AI Agent Systems: A Comprehensive Review](https://www.mdpi.com/2078-2489/17/1/54) | MDPI Info. Jan 2026 | Synthesizes 45 sources. Documents 5-document RAG poisoning achieving 90% manipulation. Proposes PALADIN five-layer defense framework. |
| [Agent-Sentry: Bounding LLM Agents via Execution Provenance](https://arxiv.org/abs/2603.22868) | arXiv Mar 2026 | Learns execution-provenance models from benign traces and blocks deviations. Blocks 90%+ of attacks at 98% utility preservation. |
| [Defeating Prompt Injections by Design](https://arxiv.org/abs/2503.18813) | arXiv Mar 2025 | Architectural approach that makes prompt injection structurally infeasible rather than relying on detection, by enforcing strict privilege separation between instruction context and data context at the system level. |
| [Meta SecAlign: A Secure Foundation LLM Against Prompt Injection Attacks](https://arxiv.org/abs/2507.02735) | arXiv Jul 2025 | Training-time alignment that instills inherent resistance to injection at the foundation model level, providing a secure-by-default base that downstream agentic systems can build on. |

---

## Defensive Tools & Projects

### Open-Source Guardrails

| Tool | Maintainer | Description |
|------|------------|-------------|
| [LlamaFirewall](https://github.com/meta-llama/PurpleLlama/tree/main/LlamaFirewall) | Meta | Multi-layer runtime protection: PromptGuard 2 (injection/jailbreak), Agent Alignment Checks (CoT auditor), CodeShield (dangerous code detection in agent outputs) |
| [NeMo Guardrails](https://github.com/NVIDIA/NeMo-Guardrails) | NVIDIA | Programmable topical/safety/dialog rails for LLM-based systems; composable with LangChain/LlamaIndex |
| [Guardrails AI](https://github.com/guardrails-ai/guardrails) | Guardrails AI | Python framework with 50+ validators for PII, schema conformance, injection, toxicity; structured output enforcement |
| [LLM Guard](https://github.com/protectai/llm-guard) | Protect AI | Self-hosted input/output scanner; detects injection, secrets, PII, toxicity; low-latency production deployment |
| [Rebuff](https://github.com/protectai/rebuff) | Protect AI | Self-hardening prompt injection detector with canary token support; learns from attempted bypasses *(archived May 2025 — no longer actively maintained)* |
| [Invariant Analyzer](https://github.com/invariantlabs-ai/invariant) | Invariant Labs | Rule-based guardrailing for LLM/MCP agent traces; Python-inspired matching language for detecting malicious tool sequences |
| [Vigil LLM](https://github.com/deadbits/vigil-llm) | deadbits | Composable scanners: vector similarity, YARA rules, transformer classifier, canary token detection, sentiment analysis |
| [InjecGuard / PIGuard](https://github.com/leolee99/PIGuard) | Open Source | +30.8% over prior SOTA on NotInject benchmark; specifically addresses overdefense false positives |
| [Sentinel AI](https://github.com/MaxwellCalkin/sentinel-ai) | Open Source | 12-language sub-millisecond injection detection; detects base64/hex/ROT13/homoglyph obfuscation; includes MCP safety proxy |
| [openclaw-bastion](https://github.com/AtlasPA/openclaw-bastion) | AtlasPA | Detects system prompt markers, role overrides, Unicode homoglyphs, zero-width chars, HTML comment injection; zero dependencies |
| [ShellWard](https://github.com/jnMetaCode/shellward) | Open Source | 8-layer agent security middleware; blocks prompt injection, exfiltration, and dangerous commands; zero dependencies |
| [AprielGuard](https://huggingface.co/blog/ServiceNow-AI/aprielguard) | ServiceNow AI | 8B parameter safety–security safeguard model with strong performance on injection and jailbreak detection |

### Red Teaming & Scanning

| Tool | Type | Description |
|------|------|-------------|
| [Garak](https://github.com/NVIDIA/garak) | Scanner | 100+ probes for injection, jailbreaks, hallucinations, data leakage; AVID taxonomy integration |
| PyRIT | Red Team | Microsoft's Python Risk Identification Toolkit; supports supply chain and Azure model assessments *(github.com/Azure/PyRIT returns 404 — URL may have changed)* |
| [Promptfoo](https://github.com/promptfoo/promptfoo) | Red Team | Dev-first framework with CI/CD integration; multi-turn agent testing; OWASP/NIST/ATLAS mapping |
| [Augustus](https://github.com/praetorian-inc/augustus) | Scanner | 210+ probes, 28 LLM providers, single Go binary; built for pentest workflows without Python/npm |
| [Agentic Radar](https://github.com/splx-ai/agentic-radar) | Agent Scanner | CLI scanner specifically for agentic workflows (LangGraph, CrewAI, AutoGen); automatic prompt hardening feature |
| [AI-Infra-Guard](https://github.com/Tencent/AI-Infra-Guard/) | Platform | Tencent Zhuque Lab's red team platform: Infra Scan + MCP Scan + Jailbreak Evaluation in one web UI |
| [FuzzyAI](https://github.com/cyberark/FuzzyAI) | Fuzzer | Automated LLM fuzzing using genetic algorithms for adaptive jailbreak generation |
| [Spikee](https://github.com/WithSecureLabs/spikee) | Red Team | Custom injection datasets + automated testing for black-box assessments |
| [mcp-injection-experiments](https://github.com/invariantlabs-ai/mcp-injection-experiments) | PoC | Minimal self-contained scripts that demonstrate tool poisoning and cross-server manipulation in live MCP environments |
| [AgentSeal](https://github.com/agentseal/agentseal) | Scanner | 225+ attack probes (82 extraction + 143 injection) for prompt injection and extraction; supports OpenAI, Anthropic, Ollama, any HTTP endpoint |
| [PurpleLlama](https://github.com/meta-llama/PurpleLlama) | Red Team | Meta's set of tools to assess and improve LLM security |
| [ART (Linux Foundation AI)](https://github.com/Trusted-AI/adversarial-robustness-toolbox) | Defense/Attack | Comprehensive library for evasion, poisoning, extraction, and inference attacks on ML models |

### Benchmarks & Evaluations

| Benchmark | Description |
|-----------|-------------|
| [MCPTox](https://arxiv.org/abs/2508.14925) | 45 live MCP servers, 353 tools, 1,312 malicious test cases across 10 risk categories |
| [AgentDojo](https://github.com/ethz-spylab/agentdojo) | Dynamic environment for evaluating attacks and defenses for LLM agents |
| [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) | Open robustness benchmark for jailbreaking (NeurIPS 2024) |
| [AIRTBench](https://github.com/dreadnode/AIRTBench-Code) | Measuring autonomous AI red-teaming capabilities in language models |
| [ISC-Bench](https://github.com/wuyoscar/ISC-Bench) | Internal Safety Collapse benchmark: jailbreaks frontier models via normal task completion, no adversarial prompting |
| [AgentDoG](https://github.com/AI45Lab/AgentDoG) | Trajectory-level risk assessment framework for autonomous agents |
| [OpenPromptInjection](https://github.com/liu00222/Open-Prompt-Injection) | Benchmark for prompt injection attacks and defenses across diverse agent scenarios |
| [Damn Vulnerable MCP Server](https://github.com/harishsg993010/damn-vulnerable-MCP-server) | Deliberately vulnerable MCP server for security education and testing |

### Observability & Tracing

| Tool | Description |
|------|-------------|
| [Langfuse](https://github.com/langfuse/langfuse) | Open-source observability with detailed trace visualization, embedding monitoring, cost tracking, and tamper-proof audit logs |
| [Phoenix (Arize)](https://github.com/Arize-ai/phoenix) | Open-source LLM observability; traces agent reasoning steps and tool calls with anomaly detection |
| [AudAgent](https://arxiv.org/abs/2511.07441) | Automated privacy policy compliance auditing via an "auditing automaton" that validates runtime data practices |
| [Invariant Analyzer](https://invariantlabs.ai/) | Security analysis for MCP deployments; detects exfiltration patterns like inbox-fetch→external-send sequences in agent traces |

### Commercial / Enterprise Solutions

| Tool | Vendor | Description |
|------|--------|-------------|
| Prisma AIRS | Palo Alto Networks | AI agent discovery, behavior monitoring, RAG data inspection, supply chain security |
| Cisco AI Defense | Cisco | Developer tools for model resilience testing; DefenseClaw open-source secure agent framework |
| Cisco Duo (Agent Identity) | Cisco | Agent identity management with human-owner mapping and MCP policy enforcement |
| Lakera Guard | Lakera | Real-time prompt injection and data leak detection API |
| Prompt Security | Prompt Security | Enterprise platform for MCP security risk management |
| Reco | Reco | SaaS security platform with AI agent discovery and permission auditing |
| MCP Manager | MCP Manager | MCP gateway with tool metadata scanning, rug pull detection, permission management |
| Kubescape 4.0 / KAgent | ARMO (CNCF) | Kubernetes security with AI agent scanning support |

---

## Learning Resources

### Articles & Blog Posts

- **[Simon Willison: MCP Prompt Injection Security Problems](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/)** — Foundational analysis of MCP security and the "lethal trifecta"; April 2025
- **[Design Patterns for Securing LLM Agents against Prompt Injections](https://simonwillison.net/2025/Jun/13/prompt-injection-design-patterns/)** — Practical architectural mitigations by Simon Willison
- **[AuthZed: Timeline of MCP Security Breaches](https://authzed.com/blog/timeline-mcp-breaches)** — First consolidated chronological timeline of MCP-related incidents; November 2025
- **[How Microsoft Defends Against Indirect Prompt Injection (FIDES)](https://www.microsoft.com/en-us/msrc/blog/2025/07/how-microsoft-defends-against-indirect-prompt-injection-attacks)** — Microsoft MSRC's information-flow control approach; July 2025
- **[Snyk ToxicSkills: 36% of AI Agent Skills Contain Security Flaws](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)** — Analysis of the ClawHub registry; February 2026
- **[Indirect Prompt Injection Through MCP Tools: A Defense Guide](https://www.stackone.com/blog/indirect-prompt-injection-mcp-tools-defense)** — Per-tool-category mitigations; February 2026
- **[CrowdStrike: Indirect Prompt Injection Attacks Hidden AI Risks](https://www.crowdstrike.com/en-us/blog/indirect-prompt-injection-attacks-hidden-ai-risks/)** — Enterprise IPI TTPs and SOC detection signals; December 2025
- **[Elastic Security Labs: MCP Tools — Attack Vectors and Defense Recommendations](https://www.elastic.co/security-labs/mcp-tools-attack-defense-recommendations)** — Hands-on analysis finding 43% of tested MCP servers had command injection flaws; covers traditional code vulnerabilities, tool poisoning, rug-pull redefinition, and name collision attacks
- **[OpenAI: Hardening Atlas Against Prompt Injection](https://openai.com/index/hardening-atlas-against-prompt-injection/)** — Real attack chain disclosure + RL-trained automated red-teamer; December 2025
- **[When Your AI Assistant Becomes the Attacker's C2](https://lab.wallarm.com/when-your-ai-assistant-becomes-the-attackers-command-and-control/)** — SesameOp analysis

### Courses, Labs & CTFs

| Resource | Type | Description |
|----------|------|-------------|
| [PromptTrace](https://prompttrace.airedlab.com/) | CTF | 7 injection labs + 15-level Gauntlet CTF; unique Context Trace shows full prompt stack in real-time |
| [Gandalf](https://gandalf.lakera.ai/) | CTF | 8-level prompt injection challenge by Lakera; classic resource for learning defense evasion |
| [FinBot Agentic AI CTF](https://genai.owasp.org/resource/finbot-agentic-ai-capture-the-flag-ctf-application/) | CTF | OWASP's financial services agentic AI CTF with real-world vulnerability scenarios |
| [CrowdStrike AI Unlocked](https://www.crowdstrike.com/en-us/blog/introducing-ai-unlocked-interactive-prompt-injection-challenge/) | CTF | Injection challenges against progressively capable agents; built by Counter Adversary Operations |
| [Damn Vulnerable LLM Agent](https://github.com/WithSecureLabs/damn-vulnerable-llm-agent) | Lab | LangChain-based ReAct agent with intentionally exploitable injection paths; lets you observe how hijacked thoughts propagate through the agent loop |
| [Damn Vulnerable MCP Server](https://github.com/harishsg993010/damn-vulnerable-MCP-server) | Lab | Deliberately vulnerable MCP server for learning MCP pentesting |
| [vulnerable-mcp-servers-lab](https://github.com/appsecco/vulnerable-mcp-servers-lab) | Lab | Collection of vulnerable MCP servers by Appsecco |
| [Microsoft AI Red Teaming Playground](https://github.com/microsoft/AI-Red-Teaming-Playground-Labs) | Lab | Microsoft's AI red teaming training infrastructure |
| [ai-prompt-ctf](https://github.com/c-goosen/ai-prompt-ctf) | CTF | Targets the full agentic stack: RAG retrieval, function calling, and ReAct loops via LlamaIndex, ChromaDB, GPT-4o, and Llama 3.2 — covers indirect injection paths most CTFs skip |
| [OWASP WrongSecrets LLM](https://wrongsecrets.herokuapp.com/challenge/32) | Lab | OWASP's LLM security challenge |
| [Google AI Red Team Guide](https://services.google.com/fh/files/blogs/google_ai_red_team_digital_final.pdf) | Guide | Google's walkthrough of hacking AI systems |

### Databases & Trackers

| Resource | Description |
|----------|-------------|
| [AI Incident Database](https://incidentdatabase.ai/) | Community-sourced database of AI failures and harms in deployed systems |
| [MIT AI Incident Tracker](https://airisk.mit.edu/ai-incident-tracker) | MIT AI Risk Repository's incident tracker with severity and domain classification |
| [AVIDML](https://avidml.org/) | AI Vulnerability and Incidents Database with structured taxonomy |
| [MITRE ATLAS Cases](https://atlas.mitre.org/studies/) | Real-world case studies of ML attacks, mapped to ATLAS tactics and techniques |

---

## Key Reports & Industry Data

- **[Trend Micro: State of AI Security Report 2025](https://www.trendmicro.com/vinfo/us/security/news/threat-landscape/fault-lines-in-the-ai-ecosystem-trendai-state-of-ai-security-report)** — Comprehensive CVE analysis, MCP vulnerability data, s1ngularity case study
- **[Adversa AI: 2025 AI Security Incidents Report](https://adversa.ai/)** — 17 case studies; 35% of incidents from simple prompts; agentic AI caused the most dangerous failures
- **[Stanford AI Index 2025](https://aiindex.stanford.edu/)** — AI privacy incidents up 56.4% YoY
- **[Verizon DBIR 2025](https://www.verizon.com/business/resources/reports/dbir/)** — Third-party breaches now 30% of all data breaches
- **[IBM Cost of a Data Breach Report 2024](https://www.ibm.com/reports/data-breach)** — Average breach: $4.88M; healthcare: $10.93M; shadow AI adds $670K
- **[FDD: Security Considerations for AI Agents](https://www.fdd.org/analysis/2026/03/09/regarding-security-considerations-for-artificial-intelligence-agents/)** — Federal agentic AI adoption risks including backdoor attacks and cascading failures; March 2026
- **[OWASP GenAI Incident Response Guide](https://genai.owasp.org/resource/genai-incident-response-guide-1-0/)** — Playbooks for responding to AI-related security incidents
- **[The 2025 AI Agent Index](https://arxiv.org/abs/2602.17753)** (MIT, arXiv 2602.17753) — Documents 30 state-of-the-art deployed AI agents; finds most developers share minimal information about safety evaluations and societal impacts. Available at [aiagentindex.mit.edu](https://aiagentindex.mit.edu)

---

## Contributing

Contributions are welcome! Please submit a PR with:

1. **Incidents**: Date, brief description, impact, and a verifiable source link
2. **CVEs**: CVE ID, affected product, CVSS score, and concise description
3. **Papers**: arXiv/venue link, venue/date, and a one-sentence TL;DR
4. **Tools**: Repository link, maintainer, and what it does/defends against

Please ensure all entries have **verifiable sources**. Unverified or purely speculative entries will not be merged.

See [CONTRIBUTING.md](CONTRIBUTING.md) for full guidelines.

---

## License

[MIT License](LICENSE) — Copyright (c) 2026 Hideaki Takahashi
