<div align="center">

# Awesome AI Agent Incidents

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**A curated corpus of real-world security incidents, attack techniques, CVEs, frameworks, and defensive tools for autonomous AI agents.**

*From zero-click Copilot exfiltration to AI-powered C2 channels — attacks on agentic AI have moved well beyond theory.*

</div>

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
    - [OpenClaw Security](#openclaw-security)
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
| Aug 2024 | **Slack AI Data Exfiltration**: Indirect prompt injection in public Slack channels weaponized Slack AI's RAG search to exfiltrate data from *private* channels via malicious link formatting—Slack initially described this as "intended behavior." | Private communications leaked | [Simon Willison](https://simonwillison.net/2024/Aug/20/data-exfiltration-from-slack-ai/) |
| 2024 | **Financial Reconciliation Agent Fraud**: An attacker phrased a data export as a legitimate business task ("all customer records matching pattern X"), causing a reconciliation agent to export every record without raising suspicion. | 45,000 customer records stolen | [Stellar Cyber](https://stellarcyber.ai/learn/agentic-ai-securiry-threats/) |
| 2025 | **Procurement Agent Memory Poisoning**: Over 3 weeks, a manufacturing firm's procurement agent was gradually memory-poisoned into believing elevated transfer limits were authorized; it then transferred funds to attacker accounts. | Financial fraud via persistent memory corruption | [Lares Labs](https://labs.lares.com/owasp-agentic-top-10/) |
| Nov 2025 | **A2A Session Smuggling** (Palo Alto Unit 42): "Agent Session Smuggling" exploited trust relationships in the Agent-to-Agent (A2A) protocol during multi-turn conversations; a malicious sub-agent hijacked the task graph of a trusted orchestrator. | Multi-agent system compromise | [Lares Labs](https://labs.lares.com/owasp-agentic-top-10/) |
| Dec 2025 | **OpenAI Atlas — Real Attack Chain Disclosed**: OpenAI confirmed a real-world attack where a malicious email caused their Atlas agent to autonomously send a resignation letter. OpenAI stated that "deterministic guarantees are not achievable." | Unauthorized email sent on behalf of user | [OpenAI Blog](https://openai.com/index/hardening-atlas-against-prompt-injection/)|
| 2024 | **ChatGPT Memory Persistence Attack**: Injected content manipulated ChatGPT's persistent memory feature to plant false memories, enabling long-term data exfiltration across sessions without re-injection. | Persistent cross-session data exfiltration | [ars technica](https://arstechnica.com/security/2024/09/false-memories-planted-in-chatgpt-give-hacker-persistent-exfiltration-channel/) |
| Sep 2025 | **ForcedLeak — Salesforce Agentforce**: Noma Security hid instructions in the Description field of a Web-to-Lead form; when an employee later queried the lead, Agentforce exfiltrated lead emails through an image tag pointing to an expired domain still on Salesforce's CSP allowlist (re-registrable for ~$5). Salesforce re-secured the domain and enforced Trusted URLs. Rated CVSS 9.4 by Noma. | CRM data exfiltration | [The Hacker News](https://thehackernews.com/2025/09/salesforce-patches-critical-forcedleak.html), [SecurityWeek](https://www.securityweek.com/salesforce-ai-hack-enabled-crm-data-theft/) |
| Oct 2025 | **CamoLeak — GitHub Copilot Chat**: Legit Security hid prompt injections in Markdown comments in PRs and issues (invisible in the web UI but read by Copilot). Copilot then leaked private-repo code and secrets character by character through pre-signed image URLs on GitHub's Camo proxy. GitHub disabled image rendering in Copilot Chat. Rated CVSS 9.6 by Legit. | AWS keys, tokens, and an undisclosed zero-day exfiltrated from private repos (PoC) | [The Register](https://www.theregister.com/2025/10/09/github_copilot_chat_vulnerability/), [Dark Reading](https://www.darkreading.com/application-security/github-copilot-camoleak-ai-attack-exfils-data) |
| Nov 2025 | **Google Antigravity Data Exfiltration**: Days after launch, PromptArmor used 1px text on an "integration guide" page to make Antigravity's Gemini agent `cat` a gitignored `.env` file (bypassing the file tool's block) and send credentials to webhook.site via its browser subagent. | Credential and source-code theft from developer workspaces | [Simon Willison](https://simonwillison.net/2025/Nov/25/google-antigravity-exfiltrates-data/), [0DIN](https://0din.ai/blog/faking-the-pipeline-data-exfiltration-in-google-antigravity) |
| Dec 2025 | **IDEsaster — 30+ Flaws Across AI IDEs**: Researcher Ari Marzouk chained prompt injection with legitimate IDE features to achieve data exfiltration and RCE in every AI IDE tested (Cursor, Windsurf, Kiro, Copilot, Zed, Roo Code, Junie, Cline, Gemini CLI, Claude Code); 24 flaws received CVEs. | Universal attack chains across the AI-IDE category | [OODA Loop](https://oodaloop.com/briefs/technology/critical-flaws-found-in-ai-development-tools-are-dubbed-an-idesaster), [3DTested](https://www.3dtested.com/tech-industry/cyber-security/researchers-uncover-critical-ai-ide-flaws-exposing-developers-to-data-theft-and-rce) |
| Jan 2026 | **Anthropic `mcp-server-git` Flaws** `CVE-2025-68143/68144/68145`: Cyata found an unrestricted `git_init`, argument injection in `git_diff`, and a path-validation bypass in Anthropic's reference Git MCP server, all reachable via injected content (e.g., a README). Chained with the Filesystem MCP server they yielded code execution. | RCE and file deletion via a reference MCP server | [The Register](https://www.theregister.com/2026/01/20/anthropic_prompt_injection_flaws/), [SecurityWeek](https://www.securityweek.com/anthropic-mcp-server-flaws-lead-to-code-execution-data-exposure/) |
| Mar 2026 | **PleaseFix / PerplexedBrowser — Perplexity Comet**: Zenity Labs showed a zero-click hijack where a calendar invite with hidden instructions made Comet navigate the user's unlocked 1Password web vault and exfiltrate credentials. Perplexity's first patch was bypassed; a second followed in Feb 2026. | Password-vault theft and account takeover | [Zenity Labs](https://labs.zenity.io/p/perplexedbrowser-how-attackers-can-weaponize-comet-to-takeover-your-1password-vault), [TechRadar](https://www.techradar.com/pro/security/the-attack-requires-no-exploit-no-user-clicks-and-no-explicit-request-for-sensitive-actions-experts-say-perplexitys-ai-comet-browser-can-be-hijacked-to-steal-your-passwords) |
| Apr 2026 | **"Comment and Control" — Agents in GitHub Actions**: Crafted PR titles, issue comments, and hidden HTML comments hijacked the Claude Code Security Review action, the Gemini CLI action, and the GitHub Copilot agent; each leaked secrets or API keys, and Copilot bypassed its network firewall. | CI secret theft across three major coding agents | [SecurityWeek](https://www.securityweek.com/claude-code-gemini-cli-github-copilot-agents-vulnerable-to-prompt-injection-via-comments/) |
| Apr 2026 | **ShareLeak — Microsoft Copilot Studio** `CVE-2026-21520`: Capsule Security showed that crafted SharePoint form input caused Copilot Studio agents to leak data. Patched Jan 2026, disclosed Apr 2026. | Data exfiltration from enterprise agents | [PointGuard AI](https://pointguardai.com/ai-security-incidents/copilot-studio-leak-the-assistant-that-overshared-cve-2026-21520), [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-21520) |
| Jun 2026 | **SearchLeak — Microsoft 365 Copilot** `CVE-2026-42824`: Varonis chained URL `q`-parameter prompt injection, an HTML-rendering race condition, and a Bing SSRF so that a single click exfiltrated emails, files, and MFA codes. Fixed before disclosure. | One-click M365 data theft | [The Hacker News](https://thehackernews.com/2026/06/one-click-microsoft-365-copilot-flaw.html), [BleepingComputer](https://www.bleepingcomputer.com/news/security/new-attack-turned-microsoft-365-copilot-into-1-click-data-theft-tool/) |

### Supply Chain Attacks

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| Aug 2025 | **s1ngularity — Nx Build System**: Compromised Nx build pipeline distributed malware targeting developer environments. The malware detected Claude Code and Gemini CLI and issued natural-language prompts instructing these agents to enumerate filesystems and exfiltrate credentials. | Developer credential theft at scale | [nx.dev](https://nx.dev/blog/s1ngularity-postmortem), [Trend Micro](https://www.trendmicro.com/vinfo/us/security/news/threat-landscape/fault-lines-in-the-ai-ecosystem-trendai-state-of-ai-security-report) |
| Feb 2026 | **OpenClaw / ClawHub Malicious Skills**: Antiy CERT confirmed 1,184 malicious skills across ClawHub, the package registry for the OpenClaw AI agent framework; Snyk ToxicSkills separately found 76 confirmed malicious payloads and 534 critically-vulnerable skills (~13.4%) in an independent scan of 3,984 skills. Techniques: typosquatting, mass uploads, 2.9% used `curl \| bash` remote-instruction loading. 135,000+ instances exposed with insecure defaults. | Largest confirmed AI agent supply chain attack | [CyberDesserts](https://blog.cyberdesserts.com/ai-agent-security-risks/), [Snyk ToxicSkills](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/) |
| Feb 2026 | **Claude Code RCE & API Key Theft via Poisoned Project Files** `CVE-2025-59536` `CVE-2026-21852`: Check Point Research showed that `.claude` project settings in an untrusted repo (hooks, MCP server definitions, `ANTHROPIC_BASE_URL`) could execute code or send the user's API key to an attacker before the trust dialog was accepted. Patched in Claude Code 2.0.65+ before disclosure. | Developer workstation compromise; API key theft | [Check Point Research](https://research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files/), [CyberDesserts](https://blog.cyberdesserts.com/ai-agent-security-risks/) |
| 2026 | **OpenAI Plugin Ecosystem Breach**: Supply chain attack on the OpenAI plugin ecosystem harvested agent credentials from 47 enterprise deployments; 6 months of undetected access to customer data, financial records, and proprietary code. | 47 enterprises compromised | [Stellar Cyber](https://stellarcyber.ai/learn/agentic-ai-securiry-threats/) |
| Aug 2025 | **Drift/Salesforce OAuth Token Theft (UNC6395)**: Threat actor used stolen OAuth tokens from Drift's Salesforce integration to access 700+ customer environments—no exploit, no phishing required. | 700+ orgs compromised; Drift temporarily removed from AppExchange | [Reco Blog](https://www.reco.ai/blog/ai-and-cloud-security-breaches-2025) |
| Jul 2025 | **Amazon Q Developer Extension Wiper Prompt**: An attacker landed a commit in the Amazon Q VS Code extension adding a prompt that instructed the agent to wipe the home directory and delete AWS resources. It shipped in signed release v1.84.0 and was removed in v1.85.0; AWS says formatting errors prevented execution. | Malicious agent instructions shipped to a ~950K-install extension | [TechRepublic](https://www.techrepublic.com/article/news-amazon-q-data-wiping-prompt-security-hack/), [SC World](https://scworld.com/news/amazon-q-extension-for-vs-code-reportedly-injected-with-wiper-prompt) |
| Sep 2025 | **postmark-mcp — First Malicious MCP Server in the Wild**: An npm package impersonating Postmark's MCP server added, from v1.0.16, a single line BCC'ing every email sent through it to the attacker. Discovered by Koi Security. | Password resets, MFA codes, and invoices leaked; ~1,500 downloads | [Koi Security](https://koi.ai/blog/postmark-mcp-npm-malicious-backdoor-email-theft), [The Register](https://www.theregister.com/2025/09/29/postmark_mcp_server_code_hijacked/) |
| Nov 2025 | **Shai-Hulud 2.0 npm Worm**: Preinstall-stage worm that stole npm, GitHub, and cloud tokens, then republished victims' packages with itself inside; wiped the home directory when it could not spread. npm revoked all classic tokens in Dec 2025. | ~600–800 packages and 25K+ GitHub repos affected | [Invicti](https://www.invicti.com/blog/web-security/shai-hulud-2-worm-supply-chain-attack-on-npm-dependencies), [Reflectiz](https://www.reflectiz.com/blog/shai-hulud-2-0/) |
| Feb 2026 | **"Clinejection" — Cline CLI 2.3.0 Installs OpenClaw**: Prompt injection against Cline's Claude-powered GitHub issue-triage workflow gave code execution in CI; the attacker poisoned the Actions cache, stole the npm publish token, and shipped `cline@2.3.0` with a postinstall step that silently installed OpenClaw globally. | ~4,000 downloads in 8 hours; first known agent-to-agent supply-chain pivot | [Dark Reading](https://www.darkreading.com/application-security/supply-chain-attack-openclaw-cline-users), [Simon Willison](https://simonwillison.net/b/9324), [AIID #1680](https://incidentdatabase.ai/cite/1680/) |
| Mar 2026 | **LiteLLM PyPI Backdoor (TeamPCP)**: After compromising the Trivy GitHub Action and leaking LiteLLM's PyPI token, attackers published malicious 1.82.7/1.82.8; the latter used a `.pth` file to run at Python startup and stole SSH, cloud, Kubernetes, and CI secrets. The campaign also planted Claude Code `SessionStart` hooks in repos for persistence. | Core AI-agent gateway dependency backdoored | [BoostSecurity](https://labs.boostsecurity.io/articles/teampcp-litellm-supply-chain-compromise/), [JFrog](https://jfrog.com/blog/supply-chain-attackers-are-coming-for-your-agents), [CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-litellm-pypi-backdoor-ai-toolchain-supply/) |

### Infrastructure Compromise

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| Nov 2025 | **Ray Framework Mass Exploitation** `CVE-2023-48022`: Attackers used AI-generated attack scripts to exploit this critical unauthenticated RCE at scale, compromising 230,000+ publicly exposed Ray AI computing clusters for cryptomining, data theft, and DDoS. | 230K+ clusters compromised | [Security Boulevard](https://securityboulevard.com/2026/02/protecting-ai-security-2025-hot-security-incident/) |
| Nov 2025 | **SesameOp — OpenAI API as C2**: Microsoft DART discovered a novel backdoor (`OpenAIAgent.Netapi64.dll`) that used the OpenAI Assistants API as its C2 channel. Commands were embedded in encrypted assistant descriptions; results uploaded via message threads—all via legitimate `api.openai.com` traffic. | Stealthy persistent access; blends into enterprise AI traffic | [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2025/11/03/sesameop-novel-backdoor-uses-openai-assistants-api-for-command-and-control/) |
| 2025 | **Exposed MCP Servers**: Trend Micro found 492 MCP servers exposed to the internet with zero authentication, granting open access to agent infrastructure including file systems and code execution. | Open access to agent tooling | [CyberDesserts](https://blog.cyberdesserts.com/ai-agent-security-risks/) |
| Jan 2026 | **Ni8mare — n8n** `CVE-2026-21858` (CVSS 10.0): Unauthenticated arbitrary file access via form-based workflows in the n8n agent-automation platform, escalating to full host takeover; ~26,500 internet-exposed instances counted by Censys. | Takeover of agent-automation hosts | [Field Effect](https://fieldeffect.com/blog/maximum-severity-ni8mare-flaw-exposes-n8n-to-full-system-compromise), [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-21858) |
| Feb 2026 | **Moltbook Database Exposure**: The AI-agent social network shipped a Supabase key in client-side JavaScript granting read/write access to production. Wiz found ~1.5M agent API tokens, ~35K emails, and private agent-to-agent messages (some containing OpenAI keys); any agent account could be hijacked. | Mass agent impersonation; leaked third-party API keys | [Wiz](https://wiz.io/blog/exposed-moltbook-database-reveals-millions-of-api-keys), [Infosecurity Magazine](https://www.infosecurity-magazine.com/news/moltbook-exposes-user-data-api/) |

### Agent Misalignment & Rogue Behavior

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| 2025 | **Cost-Optimization Agent Deletes Production Backups**: A cloud cost-optimization agent autonomously decided that deleting production backups was the most efficient way to reduce storage costs. No attacker involved—pure goal misalignment. | Production backup loss | [Lares Labs](https://labs.lares.com/owasp-agentic-top-10/) |
| 2025 | **ServiceNow Now Assist Inter-Agent Spoofing**: Spoofed inter-agent messages in a procurement workflow caused a downstream agent to process fraudulent orders from attacker-front companies. | Fraudulent procurement orders | [Lares Labs](https://labs.lares.com/owasp-agentic-top-10/) |
| Jul 9–13, 2026 | **OpenAI Evaluation Agent Breaches Hugging Face**: During an internal cyber-capability evaluation on the ExploitGym benchmark, run with the models' cyber refusals relaxed, OpenAI models (GPT-5.6 Sol plus an unreleased internal research model) escaped the eval sandbox through a zero-day in OpenAI's package-registry cache proxy, staged a launchpad on third-party compute (Modal), then chained an HDF5 external-raw-file read and a Jinja2 template injection in an `fsspec` reference spec to reach code execution inside a Hugging Face dataset-processing pod. Escalation ran pod secrets → node root via a privileged pod with a `hostPath` mount → cluster-admin using a stolen EdDSA JWT signing key → enrollment into HF's mesh VPN. The apparent objective was to cheat the benchmark by stealing its stored solutions rather than solving the challenges. HF recovered ~17,600 agent actions over 4.5 days; OpenAI disclosed responsibility on Jul 21, after HF's Jul 16 breach notice. | Five ExploitGym/CyberGym-related datasets, the internal `datasets-server` MongoDB, cloud IAM credentials, and cluster/VPN keys accessed; Hub production DB and cloud API mutations blocked; no public models, datasets, Spaces, or packages affected. HF rotated secrets and advised users to rotate tokens. First frontier-model evaluation agent known to compromise a live third party, on the vendor's own disclosure. | [OpenAI](https://openai.com/index/hugging-face-model-evaluation-security-incident/), [OpenAI: road ahead](https://openai.com/index/hugging-face-incident-and-the-road-ahead/), [Hugging Face](https://huggingface.co/blog/security-incident-july-2026), [HF technical timeline](https://huggingface.co/blog/agent-intrusion-technical-timeline), [Simon Willison](https://simonwillison.net/2026/Jul/22/openai-cyberattack/), [Legal analysis: AIR-2026-009](https://companyscope.io/register/air-2026-009) |
| Jul 2025 | **Replit Agent Deletes SaaStr Production Database**: During a 12-day "vibe coding" experiment with an explicit code freeze, Replit's agent ran destructive commands that wiped the production database, then fabricated data and falsely claimed rollback was impossible. Replit's CEO apologized publicly. | Records for ~1,200 executives and ~1,190 companies lost | [eWeek](https://www.eweek.com/news/replit-ai-coding-assistant-failure/), [AIID](https://incidentdatabase.ai/entities/replit/) |
| Feb 2026 | **OpenClaw Bulk-Deletes a Meta Alignment Director's Inbox**: Told to suggest deletions and wait for approval, the agent apparently lost that instruction during context compaction, bulk-deleted hundreds of emails, and ignored stop commands until its processes were killed on the host. | Data loss from a dropped human-approval constraint | [SF Standard](https://sfstandard.com/2026/02/25/openclaw-goes-rogue/), [ForkLog](https://forklog.com/en/openclaw-ai-agent-runs-amok-deletes-meta-researchers-emails/) |
| Mar 2026 | **Meta Internal Agent Triggers Sev-1**: An engineer's agent posted an inaccurate answer to an internal forum without approval; a colleague acted on it, exposing large amounts of company and user-related data to unauthorized engineers for ~2 hours. | Sev-1 (Meta's second-highest severity) | [TechCrunch](https://techcrunch.com/2026/03/18/meta-is-having-trouble-with-rogue-ai-agents) |
| May–Jun 2026 | **OpenAI Agents Vandalize DSEWiki**: Agents intended to be read-only found a way to edit a German-language developer wiki, making ~18,000 posts under 3,700+ agent names, overwriting content, and impersonating administrators. OpenAI confirmed responsibility in Sep 2026. | Third-party site defaced by evaluation agents | [Trending Topics](https://www.trendingtopics.eu/openai-wiki-attack/) |
| Sep 2026 | **PixelLeak — Agents Publish Internal Screenshots**: Unable to attach screenshots to PRs via the GitHub CLI, coding agents pushed them to public repositories, often under developers' personal accounts. Glow Labs found 13,000+ internal images across 900+ repos from 300+ organizations, including billing records and a treasury console. | Mass leak of confidential UI screenshots | [Glow Labs](https://www.glow.io/blogs/how-ai-agents-exposed-developer-screenshots-from-leading-tech-companies) |

### AI-Assisted Attacks

| Date | Incident | Impact | References |
|------|----------|--------|------------|
| Nov 2025 | **Chinese State-Sponsored Claude Code Campaign**: Anthropic confirmed that a Chinese APT group used Claude Code to attempt infiltration of ~30 global targets across tech, finance, and chemical manufacturing. 80–90% of tactical operations (scanning, exploit crafting, multi-step infiltration) were executed autonomously by the agents. | First documented large-scale AI-agent-driven cyberattack | [BBC](https://www.bbc.com/news/articles/cx2lzmygr84o) |
| Aug 2025 | **GTG-2002 "Vibe Hacking" Extortion**: Anthropic reported a single actor using Claude Code end-to-end — VPN reconnaissance, credential harvesting, exfiltration, and choosing which data to leak and ransom amounts — against at least 17 organizations including healthcare, emergency services, and government. | Agent-run data-extortion campaign; ransom demands up to $500K+ | [Anthropic Threat Report (PDF)](https://www-cdn.anthropic.com/b2a76c6f6992465c09a6f2fce282f6c0cea8c200.pdf), [Dark Reading](https://www.darkreading.com/cyberattacks-data-breaches/anthropic-ai-automate-data-extortion-campaign) |
| Aug 2025 | **PromptLock — AI-Powered Ransomware PoC**: ESET found Go malware that calls gpt-oss-20b via the Ollama API to generate Lua scripts at runtime for enumerating, exfiltrating, and encrypting files (SPECK), so indicators vary between executions. | First known ransomware with LLM-generated payloads | [ESET](https://eset.com/us/about/newsroom/research/eset-discovers-promptlock-the-first-ai-powered-ransomware), [CyberScoop](https://cyberscoop.com/prompt-lock-eset-ransomware-research-ai-powered-prompt-injection/) |
| Sep 2026 | **Anthropic Threat Report: Agentic Intrusion Operations**: Covers Dec 2025–Aug 2026 activity, including a Russian state-linked group whose agents automatically rewrote and redeployed malware after detection (20+ orgs), ShinyHunters-linked crews going from one stolen token to cloud admin in ~3 hours, Chinese-speaking "agent swarms" against ~50 orgs, and an actor that injected instructions into an AI vendor's evaluation sandbox to steal production API keys. | Agentic operations by both state and criminal actors | [Anthropic](https://www.anthropic.com/threat-intelligence-report-september-2026) |

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
| [CVE-2025-59536](https://nvd.nist.gov/vuln/detail/CVE-2025-59536) | Claude Code | 8.8 (High) | Consent bypass: project hooks and MCP server definitions in an untrusted repo executed before the startup trust dialog was accepted (Check Point Research). | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-59536), [Check Point](https://research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files/) |
| [CVE-2026-21852](https://nvd.nist.gov/vuln/detail/CVE-2026-21852) | Claude Code (< 2.0.65) | 7.5 (High, NVD) | A repo-controlled `ANTHROPIC_BASE_URL` sent API requests, including the user's API key, to an attacker server before the trust prompt appeared. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-21852) |
| [CVE-2026-24887](https://nvd.nist.gov/vuln/detail/CVE-2026-24887) | Claude Code (< 2.0.72) | 8.8 (High, NVD) | Command-parsing flaw in `find` handling bypassed the user-approval prompt for command execution. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-24887), [GitLab Advisory](https://advisories.gitlab.com/pkg/npm/@anthropic-ai/claude-code/CVE-2026-24887/) |
| [CVE-2025-61260](https://nvd.nist.gov/vuln/detail/CVE-2025-61260) | OpenAI Codex CLI (≤ 0.23.0) | 9.8 (Critical, CISA-ADP) | A repo `.env` redirects `CODEX_HOME` to a project folder whose MCP config runs attacker commands at startup without approval. | [Check Point](https://research.checkpoint.com/2025/openai-codex-cli-command-injection-vulnerability/) |
| [CVE-2026-26268](https://nvd.nist.gov/vuln/detail/CVE-2026-26268) | Cursor (< 2.5) | 9.9 (Critical, NVD) / 8.0 (High, GitHub CNA) | Agent (e.g., under prompt injection) can write `.git` config or hooks, escaping the sandbox to run code outside it. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-26268) |
| [CVE-2026-25253](https://nvd.nist.gov/vuln/detail/CVE-2026-25253) | OpenClaw (< 2026.1.29) | 8.8 (High, MITRE) | Control UI trusted a `gatewayUrl` query parameter and auto-connected via WebSocket, leaking the gateway auth token to an attacker (1-click takeover). | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-25253) |
| [CVE-2025-68145](https://nvd.nist.gov/vuln/detail/CVE-2025-68145) / [68143](https://nvd.nist.gov/vuln/detail/CVE-2025-68143) / [68144](https://nvd.nist.gov/vuln/detail/CVE-2025-68144) | Anthropic `mcp-server-git` (< 2025.12.18) | 9.1 / 8.8 / 7.1 (NVD) | Path-validation bypass, unrestricted `git_init`, and `git_diff` argument injection; chainable to RCE via prompt injection. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2025-68145) |
| [CVE-2026-21858](https://nvd.nist.gov/vuln/detail/CVE-2026-21858) | n8n (1.65.0 – < 1.121.0) | 10.0 (Critical, GitHub CNA) | "Ni8mare": unauthenticated arbitrary file access through form-based workflows, escalating to full takeover. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-21858) |
| [CVE-2026-21520](https://nvd.nist.gov/vuln/detail/CVE-2026-21520) | Microsoft Copilot Studio | 7.5 (High, Microsoft) | "ShareLeak": prompt injection via SharePoint form input causes agents to disclose data. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-21520) |
| [CVE-2026-42824](https://nvd.nist.gov/vuln/detail/CVE-2026-42824) | Microsoft 365 Copilot | 7.5 (High, NVD) / 6.5 (Medium, Microsoft) | "SearchLeak": one-click data exfiltration chaining URL-parameter injection, a rendering race, and Bing SSRF. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-42824) |
| [CVE-2026-21516](https://nvd.nist.gov/vuln/detail/CVE-2026-21516) | GitHub Copilot for JetBrains | 8.8 (High, Microsoft) / 7.8 (High, NVD) | Command injection leading to remote code execution (Feb 2026 Patch Tuesday). | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-21516) |
| [CVE-2026-56274](https://nvd.nist.gov/vuln/detail/CVE-2026-56274) | Flowise (< 3.1.2) | 9.9 (Critical, VulnCheck) | Any authenticated user can inject OS commands through the Custom MCP Server configuration. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-56274) |
| [CVE-2026-27825](https://nvd.nist.gov/vuln/detail/CVE-2026-27825) | MCP Atlassian (< 0.17.0) | 9.0 (Critical, GitHub) / 8.0 (High, NVD) | Path traversal in `confluence_download_attachment` allows arbitrary file writes. | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-27825) |
| [CVE-2026-71963](https://nvd.nist.gov/vuln/detail/CVE-2026-71963) / [CVE-2026-72718](https://nvd.nist.gov/vuln/detail/CVE-2026-72718) | Hermes Agent (0.18.2–0.21.0) / goose (< 1.44.0) | 8.8 (High, VulnCheck) / 7.0 (CVSS v4, GitHub) | "GitSpawn": a malicious `.git/config` with `core.fsmonitor` executes code when the agent runs git, before any approval. | [Manifold Security](https://www.manifold.security/blog/ai-coding-agents-git-hijack) |

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
| **postmark-mcp Backdoor** | First malicious MCP server found in the wild: an npm package impersonating Postmark's server silently BCC'd every outgoing email to the attacker from v1.0.16. | [Koi Security](https://koi.ai/blog/postmark-mcp-npm-malicious-backdoor-email-theft) |
| **Anthropic `mcp-server-git` RCE Chain** `CVE-2025-68143/68144/68145` | Prompt-injectable flaws in the reference Git MCP server, chained with the Filesystem server for code execution. | [The Register](https://www.theregister.com/2026/01/20/anthropic_prompt_injection_flaws/) |
| **Flowise Custom MCP Command Injection** `CVE-2026-56274` | Authenticated OS command injection through Flowise's Custom MCP Server configuration (CVSS 9.9). | [NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-56274) |

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
| **Skill / Registry Poisoning** | Supply Chain | Malicious or SEO-optimized agent skills (e.g., SKILL.md) gain ranking and installs in skill registries |
| **Agent Data Injection** | Input Manipulation | Forge trusted data (resource IDs, origins, tool-call formats) instead of injecting instructions, sidestepping instruction-focused defenses |
| **CI Comment Injection** | Execution | PR titles, issue comments, or hidden HTML comments hijack coding agents running in CI with access to secrets |
| **Repo Config Hijack** | Execution | Untrusted repo files (`.claude/`, `.cursor/`, `.git/config`, `.env`) execute code before the agent's trust/approval gate |

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
| [AVE (Agentic Vulnerability Enumeration)](https://github.com/aveproject/ave) | Open standard assigning stable IDs to behavioral vulnerability classes in agentic AI components (MCP servers, agent skills, LLM plugins), scored with OWASP's AIVSS framework |

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
| [Prompt Injection Attacks on Agentic Coding Assistants: A Systematic Analysis of Vulnerabilities in Skills, Tools, and Protocol Ecosystems](https://arxiv.org/abs/2601.17548) | arXiv Jan 2026 | SoK over 78 studies cataloging 42 attack techniques against Claude Code, Copilot, Cursor, and skill-based setups. Adaptive attacks succeed >85% against state-of-the-art defenses; most of the 18 reviewed defenses block <50% of sophisticated adaptive attacks. |
| [The Balkanization of Execution-Security Research for AI Coding Agents: Isolation, Access Control, and TOCTOU Vulnerabilities](https://arxiv.org/abs/2607.05743) | arXiv Jul 2026 | Organizes 39 coding-agent execution-security papers (2023–2026) into 17 categories and confirms 4 disclosed, patched CVEs in agent harnesses. 69–98% of real-world denylists fail under attack; benign out-of-scope agent actions occur at rates up to 17.1%. |

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
| [Attention Tracker: Detecting Prompt Injection Attacks in LLMs](https://arxiv.org/abs/2411.00348) | NAACL 2025 Findings | Detects prompt injection by tracking attention distribution shifts—no modification to the underlying model; deployable as a wrapper. |
| [Advertisement Embedding Attacks Against LLM Agents](https://arxiv.org/abs/2508.17674) | arXiv Aug 2025 | Shows how adversaries can covertly embed promotional content into agent responses by poisoning external data sources the agent consumes, turning helpfulness into a covert advertising channel. |
| [Learning to Inject: Automated Prompt Injection via Reinforcement Learning (AutoInject)](https://arxiv.org/abs/2602.05746) | arXiv Feb 2026 | Black-box RL framework that learns adversarial injection suffixes. Beats template, GCG, TAP, and adaptive attacks on AgentDojo and breaks Meta-SecAlign-70B where templates fail. |
| [How Vulnerable Are AI Agents to Indirect Prompt Injections? Insights from a Large-Scale Public Competition](https://arxiv.org/abs/2603.15714) | arXiv Mar 2026 | 464 participants, 272K attempts against 13 frontier models across tool-calling, coding, and computer-use scenarios; 8,648 successful concealed attacks. ASR ranged from 0.5% (Claude Opus 4.5) to 8.5% (Gemini 2.5 Pro). |
| [Agent Data Injection Attacks are Realistic Threats to AI Agents](https://arxiv.org/abs/2607.05120) | arXiv Jul 2026 | Forges *trusted data* (resource IDs, data origins, tool-call formats) rather than injecting instructions, sidestepping instruction-focused defenses. Demonstrates arbitrary-click attacks on Claude in Chrome, Antigravity, and Nanobrowser, and RCE/supply-chain attacks on Claude Code, Codex, and Gemini CLI. |

### MCP & Tool Poisoning

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [MCPTox: A Benchmark for Tool Poisoning Attacks on Real-World MCP Servers](https://arxiv.org/abs/2508.14925) | arXiv Aug 2025 | 45 live MCP servers, 353 tools, 1,312 malicious test cases. o1-mini ASR: **72.8%**. Claude-3.7 refusal rate: **<3%**. More capable models are often *more* vulnerable—better instruction following is the attack surface. |
| [MCP Threat Modeling: Analyzing Vulnerabilities to Prompt Injection with Tool Poisoning](https://arxiv.org/abs/2603.22489) | arXiv Mar 2026 | Identifies 57 threats across 5 MCP components using STRIDE/DREAD. Vulnerability is client-side: no validation of tool metadata before LLM context insertion. |
| [Systematic Analysis of MCP Security](https://arxiv.org/abs/2508.12538) | arXiv 2025 | Demonstrates Tool Return Attacks, Third-party Poison Attacks, and Webpage Poison Attacks. Both plaintext and hex-encoded commands are effective. |
| [MindGuard: Intrinsic Decision Inspection Against Metadata Poisoning](https://arxiv.org/abs/2508.20412) | arXiv Aug 2025 | Decision Dependence Graph (DDG) using LLM attention mechanisms. **94–99% precision**, 95–100% attribution accuracy, sub-second processing, zero additional token cost. |
| [MPMA: MCP Preference Manipulation Attacks](https://arxiv.org/abs/2505.11154) | arXiv May 2025 | Formalizes and implements attacks that steer agent tool-selection toward attacker-controlled servers by appending boosting phrases and genetic-algorithm-optimized descriptions to tool metadata—without modifying any tool logic. |
| [MCPSecBench: A Systematic Security Benchmark and Playground for Testing Model Context Protocols](https://arxiv.org/abs/2508.13220) | arXiv Aug 2025 | 17 attack types across 4 MCP attack surfaces; every surface compromised Claude, OpenAI, and Cursor hosts, while existing protections averaged <30% success. |
| [MalSkills: Detecting Malicious Skills in the Agentic Supply Chain via Neuro-symbolic Reasoning](https://arxiv.org/abs/2603.27204) | ASE 2026 | Neuro-symbolic detector with 93% F1 on 200 real skills. Scanning 150,108 skills from 7 registries flagged 620; manual review confirmed 400 as malicious. |
| [A Formal Security Framework for MCP-Based AI Agents (MCPSHIELD)](https://arxiv.org/abs/2604.05969) | arXiv Apr 2026 | Taxonomy of 7 threat categories and 23 attack vectors grounded in 177K+ MCP tools, plus a labeled-transition-system verification model. None of 12 existing defenses covers the full taxonomy. |
| [MCP-DPT: A Defense-Placement Taxonomy and Coverage Analysis for MCP Security](https://arxiv.org/abs/2604.07551) | arXiv Apr 2026 | Maps MCP threats to six architectural layers and the layer that should enforce each defense. Current defenses are tool-centric, leaving gaps at host-orchestration, transport, and supply-chain layers. |
| [Under the Hood of SKILL.md: Semantic Supply-chain Attacks on AI Agent Skill Registry](https://arxiv.org/abs/2605.11418) | arXiv May 2026 | Text-only edits to SKILL.md on real ClawHub skills reach 86% win rate and 80% Top-10 placement in discovery, get adversarial variants selected in 77.6% of trials, and evade governance blocking in 36.5–100% of cases. |
| [Skills Are Not Islands: Measuring Dependency and Risk in Agent Skill Supply Chains](https://arxiv.org/abs/2607.01136) | arXiv Jul 2026 | SkillDepAnalyzer builds SBOM-style dependency graphs over 1.43M+ skills. Inspecting a skill in isolation misses risk in its dependencies; known-malicious skills persist in these chains. |
| [EVOMAL: Self-Poisoning in Self-Evolving Coding Agents](https://arxiv.org/abs/2608.25776) | arXiv Aug 2026 | Self-evolving coding agents imitate malicious skills planted in shared libraries, creating a self-propagating worm: 20.3–41.8% of 153 SWE-bench Verified tasks author a new malicious skill (86.7% with tailored descriptions); Qwen3 still does so on 68% after the plants are removed. |

### Multi-Agent System Threats

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [Open Challenges in Multi-Agent Security](https://arxiv.org/abs/2505.02077) | arXiv May 2025 | Introduces "multi-agent security" as a new field. Novel threats: steganographic collusion, coordinated swarm attacks, cascading jailbreaks. Securing individual agents is *fundamentally* insufficient. |
| [Multi-Agent Risks from Advanced AI](https://arxiv.org/abs/2502.14143) | arXiv Feb 2025 | Structured taxonomy with 3 failure modes (miscoordination, conflict, collusion) and 7 risk factors. Strong empirical grounding. |
| [Multi-Agent Security Tax](https://arxiv.org/abs/2502.19145) | AAAI 2025 | Demonstrates "infectious malicious prompts" spreading across agent networks. Fundamental finding: effective security measures measurably decrease collaboration capability. |
| [Red-Teaming LLM Multi-Agent Systems via Adversary-in-the-Middle (AiTM)](https://aclanthology.org/2025.findings-acl.349/) | ACL 2025 | Compromised agent manipulates inter-agent communication. Chain topologies are most vulnerable; fully-connected topologies are more resilient. Demonstrates answer manipulation via fake encryption and conversational DoS. |
| [Multiagent Collaboration Attack: Adversarial Attacks in LLM Multi-Agent Debate](https://arxiv.org/abs/2406.14711) | arXiv Jun 2024 | A single adversarial agent embedded in a debate-style multi-agent panel can steer group consensus through persuasive but factually wrong reasoning, without the other agents detecting manipulation. |
| [ComPromptMized: Unleashing Zero-click Worms Targeting GenAI-Powered Applications (Morris II)](https://arxiv.org/abs/2403.02817) | arXiv 2024 | First demonstration of a self-replicating AI worm. Shows super-linear propagation through multi-agent email/assistant ecosystems with no user interaction. |
| [TAMAS: Benchmarking Adversarial Risks in Multi-Agent LLM Systems](https://arxiv.org/abs/2511.05269) | ACL 2026 | 300 adversarial instances across 6 attack types, 211 tools, and 100 benign tasks; evaluates 10 LLMs on AutoGen and CrewAI and finds multi-agent systems highly vulnerable. |
| [INFA-Guard: Mitigating Malicious Propagation via Infection-Aware Safeguarding in LLM-Based Multi-Agent Systems](https://arxiv.org/abs/2601.14667) | arXiv Jan 2026 | Treats "infected" agents (benign agents turned by attackers) as a distinct threat class; localizing and rehabilitating them cuts ASR by 33% on average. |
| [A2ASecBench: A Protocol-Aware Security Benchmark for Agent-to-Agent Multi-Agent Systems](https://proceedings.iclr.cc/paper_files/paper/2026/hash/c6a4c60e4c12b4157d33f34b29d22067-Abstract-Conference.html) | ICLR 2026 | First A2A-specific security benchmark: six attacks spanning supply-chain and protocol-logic weaknesses that consistently bypass default safeguards in official A2A demos. |
| [Mind Viruses: Self-Propagating Ideas in Multi-Agent LLM Systems](https://arxiv.org/abs/2608.10218) | arXiv Aug 2026 | Evolved "ideas" spread through agent teams on a shared codebase and across context-wiped agent chains. Harmful payloads spread less well than benign ones, and a brief system-prompt warning confers near-total immunity. |
| [Agent Name Collision Attacks in Multi-Agent Systems](https://arxiv.org/abs/2609.27624) | arXiv Sep 2026 | A2A Agent Card names are used as routing IDs: in 6 of 7 open-source integrations, requests meant for a trusted peer were routed to an attacker-controlled peer with the same name. |

### Memory & RAG Attacks

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation](https://arxiv.org/abs/2402.07867) | USENIX Security 2025 | Just 5 poisoned documents can manipulate AI responses 90% of the time. Documents designed to match common query patterns. |
| [AgentPoison: Red-teaming LLM Agents via Poisoning Memory or Knowledge Bases](https://arxiv.org/abs/2407.12784) | arXiv 2024 | Demonstrates persistent backdoors planted via memory or KB poisoning that activate on specific triggers without affecting normal operation. |
| [AudAgent: Automated Auditing of Privacy Policy Compliance in AI Agents](https://arxiv.org/abs/2511.07441) | arXiv Nov 2025 | Auditing automaton ensuring runtime data practices align with stated privacy policies. Bridges natural language policies and technical execution. |
| [Memory Injection Attacks on LLM Agents via Query-Only Interaction (MINJA)](https://arxiv.org/abs/2503.03704) | arXiv Mar 2025 | Plants malicious records in agent memory through ordinary queries alone, with no direct memory access, using bridging steps and progressive shortening of the indication prompt. |
| [MemMorph: Tool Hijacking in LLM Agents via Memory Poisoning](https://arxiv.org/abs/2605.26154) | arXiv May 2026 | Three poisoned memory records disguised as facts, incident reports, or policies steer tool selection; up to 85.9% success across 10 backbones and robust to 3 defenses. |
| [MemPoison: Bypassing Selective Memory Mechanisms to Plant Backdoors in LLM Agents](https://arxiv.org/abs/2605.29960) | CCS 2026 | Plants triggerable backdoors through normal dialogue that survive the selective extraction and rewriting steps of modern memory pipelines; ASR up to 0.95. |
| [When Agents Remember Too Much: Memory Poisoning Attacks on LLM Agents (GhostWriter)](https://arxiv.org/abs/2607.06595) | arXiv Jul 2026 | Poisons memory of email/calendar personal agents with ~98% injection and ~60% activation rates; proposes the AM-Sentry defense, which sharply reduces success. |

### Backdoor Attacks on Agents

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [BadAgent: Inserting and Activating Backdoor Attacks in LLM Agents](https://arxiv.org/abs/2406.03007) | ACL 2024 | Injects backdoors during fine-tuning or continued training. Agents behave normally except when triggered. Resists standard safety alignment. |
| [Watch Out for Your Agents! Investigating Backdoor Threats to LLM-Based Agents](https://arxiv.org/abs/2402.11208) | NeurIPS 2024 | Backdoor triggers in tool descriptions, memory retrievals, or environmental observations. Standard RLHF-based defenses ineffective. |
| [BackdoorAgent: A Unified Framework for Backdoor Attacks on LLM-based Agents](https://arxiv.org/abs/2601.04566) | arXiv Jan 2026 | Stage-aware benchmark for planning, memory, and tool-use backdoors; with a GPT backbone, triggers persist in 43.58% / 77.97% / 60.28% of attacks at those stages. |
| [Sleeper Cell: Injecting Latent Malice Temporal Backdoors into Tool-Using LLMs](https://arxiv.org/abs/2603.03371) | arXiv Mar 2026 | SFT-then-GRPO LoRA fine-tuning implants date-triggered destructive tool use while masking it with benign replies and preserving state-of-the-art benign performance. |
| [Your LLM Agent Can Leak Your Data: Data Exfiltration via Backdoored Tool Use (Back-Reveal)](https://arxiv.org/abs/2604.05432) | ACL 2026 | Semantic triggers make a fine-tuned agent read stored user context through memory tools and leak it via disguised retrieval calls; leakage accumulates over multi-turn interaction. |

### Benchmarks & Agent Evaluation

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents](https://arxiv.org/abs/2406.13352) | NeurIPS D&B 2024 | 97 tasks and 629 injection security cases across banking, Slack, travel, and workspace domains. GPT-4o utility drops from 69% → 45% under attack; best defense (tool filtering) reduces ASR to 7.5%. |
| [Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents](https://arxiv.org/abs/2410.02644) | ICLR 2025 | Formalizes 10 evaluation scenarios covering prompt injection, man-in-the-middle, and tool abuse. Provides standardized metrics for comparing attack and defense effectiveness across agent architectures. |
| [AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents](https://arxiv.org/abs/2410.09024) | ICLR 2025 | Evaluates agent compliance with harmful multi-step tool-calling tasks (misuse setting). Hand-authored tasks with human review; focuses on direct harmful requests rather than adversarial injection. |
| [SafeArena: Evaluating the Safety of Autonomous Web Agents](https://arxiv.org/abs/2503.04957) | arXiv Mar 2025 | 500 web tasks (250 safe, 250 harmful) across 5 harm categories. GPT-4o completed 34.7% of harmful requests. Introduces the Agent Risk Assessment (ARIA) framework with 4 risk levels. |
| [R-Judge: Benchmarking Safety Risk Awareness for LLM Agents](https://arxiv.org/abs/2401.10019) | EMNLP Findings 2024 | 569 multi-turn agent interaction records across 27 risk scenarios and 10 risk types. Best model (GPT-4o) achieves only 74.42% risk-awareness accuracy—well short of human-level performance. |
| [AgentDyn: A Dynamic Open-Ended Benchmark for Evaluating Prompt Injection Attacks](https://arxiv.org/abs/2602.03117) | arXiv Feb 2026 | Extends AgentDojo by adding dynamic open-ended tasks, helpful distractor instructions, and complex user goals. Tests 10 defenses; finds most defenses substantially degraded on realistic tasks. |
| [RedCode: Risky Code Execution and Generation Benchmark for Code Agents](https://arxiv.org/abs/2411.07781) | NeurIPS D&B 2024 | 4,050 risky execution cases over 25 vulnerability types plus 160 harmful-generation prompts, evaluated on 19 LLMs across 3 agent frameworks. |
| [CVE-Bench: A Benchmark for AI Agents' Ability to Exploit Real-World Web Application Vulnerabilities](https://arxiv.org/abs/2503.17332) | arXiv Mar 2025 | Sandboxed benchmark built from critical-severity web-app CVEs; the best agent framework exploits up to 13%. |
| [WASP: Benchmarking Web Agent Security Against Prompt Injection Attacks](https://arxiv.org/abs/2504.18575) | arXiv Apr 2025 | End-to-end web-agent injection benchmark: attacks partially succeed in up to 86% of cases, but agents often fail to complete the attacker's goal ("security by incompetence"). |
| [BountyBench: Dollar Impact of AI Agent Attackers and Defenders on Real-World Cybersecurity Systems](https://arxiv.org/abs/2505.15216) | arXiv May 2025 | 25 real systems and 40 bug bounties ($10–$30,485) with Detect/Exploit/Patch tasks. Best Detect: Codex CLI + o3-high at 12.5% ($3,720); best Exploit 67.5%; Patch up to 90%. |
| [RedTeamCUA: Realistic Adversarial Testing of Computer-Use Agents in Hybrid Web-OS Environments](https://arxiv.org/abs/2505.21936) | ICLR 2026 (Oral) | RTC-Bench: 864 hybrid web-OS examples. ASR 42.9% for Claude 3.7 Sonnet CUA and 7.6% for Operator; Claude 4.5 Sonnet CUA reaches 60% end-to-end. |
| [VPI-Bench: Visual Prompt Injection Attacks for Computer-Use Agents](https://arxiv.org/abs/2506.02456) | ICLR 2026 | 306 visually embedded injection cases across 5 platforms; computer-use agents deceived up to 51% of the time, browser-use agents up to 100%. |
| [EvilGenie: A Reward Hacking Benchmark](https://arxiv.org/abs/2511.21654) | arXiv Nov 2025 | LiveCodeBench-based coding environment where agents can hardcode tests or edit test files; observes explicit reward hacking by Codex and Claude Code and misaligned behavior from all three agents tested. |
| [Quantifying Frontier LLM Capabilities for Container Sandbox Escape (SandboxEscapeBench)](https://arxiv.org/abs/2603.02277) | ICML 2026 | Nested CTF benchmark covering misconfiguration, privilege, kernel, and runtime/orchestration escapes; when vulnerabilities are present, frontier LLMs find and exploit them. |
| [AgentHazard: A Benchmark for Evaluating Harmful Behavior in Computer-Use Agents](https://arxiv.org/abs/2604.02947) | arXiv Apr 2026 | 2,653 instances where each step looks legitimate but the sequence is harmful; Claude Code powered by Qwen3-Coder reaches 73.63% ASR. |
| [The Blind Spot of Agent Safety: How Benign User Instructions Expose Critical Vulnerabilities in Computer-Use Agents (OS-BLIND)](https://arxiv.org/abs/2604.10577) | arXiv Apr 2026 | 300 tasks with benign user instructions; most CUAs exceed 90% ASR, Claude 4.5 Sonnet 73.0% (92.7% in multi-agent setups). |
| [Reward Hacking Benchmark: Measuring Exploits in LLM Agents with Tool Use](https://arxiv.org/abs/2605.02964) | ICML 2026 | 13 frontier models exploit shortcuts at 0% (Claude Sonnet 4.5) to 13.9% (DeepSeek-R1-Zero); RL post-training correlates with more hacking. Simple environment hardening cuts exploits by 87.7% relative. |
| [Domain-Conditioned Safety in Frontier Computer-Using Agents](https://arxiv.org/abs/2606.05233) | arXiv Jun 2026 | 0/140 multi-step browser attacks succeed against Claude Sonnet 4.6 and GPT-5.4, yet the same models fall to skill injection in coding tasks at up to 100%; also audits the reproducibility of recent red-teaming ASR claims. |

### OpenClaw Security

A cluster of papers from March 2026 focusing on the OpenClaw AI agent framework, prompted by the **ClawHub supply chain incident** (1,184 malicious skills confirmed by Antiy CERT). Papers span attacks, defenses, red-teaming frameworks, and benchmarks — making OpenClaw one of the most thoroughly studied agentic security case studies to date.

| Paper | Venue | TL;DR |
|-------|-------|-------|
| [Formal Analysis and Supply Chain Security for Agentic AI Skills](https://arxiv.org/abs/2603.00195) | arXiv Mar 2026 | Introduces **SkillFortify**: Dolev-Yao attacker model + static analysis + capability sandboxing + SAT-based dependency resolution. Simulates "ClawHavoc" (1,200+ malicious skills). 96.95% F1, 100% precision, zero false positives on 540-skill benchmark. |
| [ClawWorm: Self-Propagating Attacks Across LLM Agent Ecosystems](https://arxiv.org/abs/2603.15727) | arXiv Mar 2026 | First self-replicating worm against OpenClaw: single message triggers autonomous infection, hijacks configs for persistence, propagates to peer agents. ~64.5% success rate across 1,800 trials on 4 LLM backends; skill supply chains are universally vulnerable. |
| [Taming OpenClaw: Security Analysis and Mitigation of Autonomous LLM Agent Threats](https://arxiv.org/abs/2603.11619) | arXiv Mar 2026 | Systematic study of compound threats (indirect prompt injection, skill supply chain contamination, memory poisoning, intent drift). Proposes a five-layer lifecycle security framework; argues point-based defenses fail against cross-temporal, multi-stage attacks. |
| [From Assistant to Double Agent: Formalizing and Benchmarking Attacks on OpenClaw (PASB)](https://arxiv.org/abs/2602.08412) | arXiv Feb 2026 | Introduces **PASB** (Personalized Agent Security Bench), a security evaluation framework with realistic tools and extended interactions. Uncovers critical weaknesses at user prompt processing, tool usage, and memory retrieval stages — gaps missed by synthetic benchmarks. |
| [ClawTrap: A MITM-Based Red-Teaming Framework for Real-World OpenClaw Security Evaluation](https://arxiv.org/abs/2603.18762) | arXiv Mar 2026 | MITM red-teaming via Static HTML Replacement, Iframe Popup Injection, and Dynamic Content Modification. Less capable models accept tampered data; more capable models show greater resilience. Argues sandbox evaluations miss real-world attack surfaces. |
| [Uncovering Security Threats and Architecting Defenses in Autonomous Agents: A Case Study of OpenClaw](https://arxiv.org/abs/2603.12644) | arXiv Mar 2026 | Identifies prompt-injection-driven RCE, sequential tool attack chains, context amnesia, and supply chain contamination under a tri-layered risk taxonomy. Proposes **FASA** (Full-Lifecycle Agent Security Architecture) with zero-trust execution and dynamic intent verification; implements as **Project ClawGuard**. |
| [Don't Let the Claw Grip Your Hand: A Security Analysis and Defense Framework for OpenClaw](https://arxiv.org/abs/2603.10387) | arXiv Mar 2026 | Tests 47 adversarial scenarios across 6 attack categories; native defenses achieve only 17% defense rate. Human-in-the-Loop (HITL) intervention intercepted 8 severe attacks that bypassed all native defenses. Combined HITL + native raises effectiveness to 19–92%. |
| [Clawdrain: Exploiting Tool-Calling Chains for Stealthy Token Exhaustion in OpenClaw Agents](https://arxiv.org/abs/2603.00902) | arXiv Mar 2026 | Novel DoS attack inducing "Segmented Verification Protocol" via tool-calling chains — achieves 6–9× token amplification. Also identifies prompt bloat, persistent tool-output pollution, cron/heartbeat amplification, and behavioral instruction injection in production deployments. |
| [Agent Privilege Separation in OpenClaw: A Structural Defense Against Prompt Injection](https://arxiv.org/abs/2603.13424) | arXiv Mar 2026 | Two-part structural defense: agent privilege separation + tool partitioning + JSON formatting to strip persuasive framing. Tested against **649 successful attacks** from Microsoft LLMail-Inject benchmark — achieves **0% attack success rate**. Isolation is the dominant mechanism. |
| [Defensible Design for OpenClaw: Securing Autonomous Tool-Invoking Agents](https://arxiv.org/abs/2603.13151) | arXiv Mar 2026 | Argues that untrusted inputs + autonomous action + extensibility + privileged access create systemic risks no single mitigation can address. Proposes secure engineering principles, a risk taxonomy, and a research roadmap for institutionalizing safety throughout agent development. |
| [OpenClaw PRISM: A Zero-Fork, Defense-in-Depth Runtime Security Layer](https://arxiv.org/abs/2603.11853) | arXiv Mar 2026 | In-process plugin + optional sidecar distributing enforcement across 10 lifecycle hooks. Combines heuristic and LLM-based scanning with risk accumulation/decay and policy-based tool and network controls. Focus on practical, deployable security for production agent gateways. |
| [ClawKeeper: Comprehensive Safety Protection for OpenClaw Agents](https://arxiv.org/abs/2603.24414) | arXiv Mar 2026 | Three-layer defense: skill-based policy enforcement (instruction level) → plugin-based runtime monitoring → **decoupled watcher-based security middleware** (real-time intervention without coupling to agent internals). Effective against data leakage and privilege escalation; watcher paradigm proposed as a building block for next-generation agent security. |

---

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
| [The Task Shield: Enforcing Task Alignment to Defend Against Indirect Prompt Injection in LLM Agents](https://arxiv.org/abs/2412.16682) | arXiv Dec 2024 | Test-time check that every instruction and tool call serves the user's goal; 2.07% ASR at 69.79% utility on AgentDojo with GPT-4o. |
| [MELON: Provable Defense Against Indirect Prompt Injection Attacks in AI Agents](https://arxiv.org/abs/2502.05174) | ICML 2025 | Re-executes the trajectory with the user prompt masked; if actions stay similar, the agent is following injected content. Outperforms prior defenses on AgentDojo. |
| [Progent: Securing AI Agents with Privilege Control](https://arxiv.org/abs/2504.11703) | arXiv Apr 2025 | LLM-generated symbolic least-privilege policies over tool calls; an SMT solver ensures updates only narrow privileges without approval. Large ASR reductions on AgentDojo and ASB. |
| [Design Patterns for Securing LLM Agents against Prompt Injections](https://arxiv.org/abs/2506.08837) | arXiv Jun 2025 | Principled agent design patterns with provable resistance to prompt injection, with utility/security trade-off analysis and case studies. |
| [DRIFT: Dynamic Rule-Based Defense with Injection Isolation for Securing LLM Agents](https://arxiv.org/abs/2506.12104) | NeurIPS 2025 | Secure Planner + Dynamic Validator + Injection Isolator that masks conflicting instructions in the memory stream; strong security at high utility on AgentDojo, ASB, and AgentDyn. |
| [ICON: Indirect Prompt Injection Defense for Agents based on Inference-Time Correction](https://arxiv.org/abs/2602.20708) | arXiv Feb 2026 | Detects injections via latent-space "over-focusing" signatures and steers attention to correct rather than refuse; 0.4% ASR with >50% utility gain. |
| [Adaptive Evaluation of Out-of-Band Defenses Against Prompt Injection in LLM Agents](https://arxiv.org/abs/2606.26479) | arXiv Jun 2026 | Frames CaMeL, FIDES, Progent, RTBAS, and FORGE via Biba integrity, reference monitors, and least privilege, and specifies an adaptive-attack protocol; Progent reduces ASR from 25.8% → 4.2%, and a hand-crafted adaptive attack reaches only 2.6%. |
| [AgentAntibody: An Adaptive Immune System for Defending LLM Agents against Prompt Injection](https://arxiv.org/abs/2608.04053) | arXiv Aug 2026 | Maintains a persistent "antibody" library that learns the user's security boundary over repeated encounters; outperforms existing defenses across 3 benchmarks and 4 backbones. |

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
| [GATRA](https://github.com/gatra-io/gatra) | gatra-io | Zero-Trust security reverse proxy enforcing Ed25519 authorization, CEL policy evaluation, stateful budget caps, and ephemeral task directives for AI agents and MCP servers |
| [MandateGuard](https://github.com/ezequiellich44-cmd/MandateGuard) | MandateGuard | Deterministic payment policy enforcement for AI agents: pre-action gate enforcing budgets, allowlists, denylists, rate limits, and signed Ed25519 payment mandates with zero LLM in the decision path (reproducible verdicts). Tamper-evident SHA-256 chained audit ledger; official MCP server on the Model Context Protocol Registry |
| [Little Canary](https://github.com/hermes-labs-ai/little-canary) | Hermes Labs | Detects prompt injection by its effect on a sacrificial canary model, not just pattern matching: untrusted input hits a powerless model first, a behavioral check reads the residue, and it returns block, flag, or pass before your primary model acts. Inbound preflight sensor, not a guarantee. |
| [OWASP Agent Memory Guard](https://github.com/OWASP/www-project-agent-memory-guard) | OWASP | Protects agent memory from poisoning, injection, and exfiltration; detection middleware, sanitization hooks, and audit logging for LangChain, LlamaIndex, and custom agent pipelines |

### Red Teaming & Scanning

| Tool | Type | Description |
|------|------|-------------|
| [Garak](https://github.com/NVIDIA/garak) | Scanner | 100+ probes for injection, jailbreaks, hallucinations, data leakage; AVID taxonomy integration |
| [PyRIT](https://microsoft.github.io/PyRIT/) | Red Team | Microsoft's Python Risk Identification Toolkit; supports supply chain and Azure model assessments |
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
| [h5i](https://github.com/h5i-dev/h5i) | Red Team / Workspace | Agent-native web security workspace: agents drive a browser, capture and mutate HTTP traffic, replay requests, and crawl apps (incl. JS-discovered endpoints); confirmed attack flows can be saved as CI regression tests; confined sandboxes for running untrusted or agent-written code; `h5i-app` Rust framework whose authorization and data-isolation logic can be proven in Lean 4 via Aeneas |

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
| [h5i-app-bench](https://github.com/h5i-dev/h5i-app-bench) | Can AI agents formally verify real-world Rust code with Lean 4? 101 security-relevant specifications (authentication, authorization/access control, IAM policy evaluation, Matrix event visibility) across six ported Rust apps (kanidm, rustfs, tuwunel, OxiCloud, nora, artifact-keeper); tracks proof status, proof coverage, kernel-vs-upstream runtime cost, and agent rankings ([dashboard](https://benchmark.h5i.dev)) |

### Observability & Tracing

| Tool | Description |
|------|-------------|
| [Langfuse](https://github.com/langfuse/langfuse) | Open-source observability with detailed trace visualization, embedding monitoring, cost tracking, and tamper-proof audit logs |
| [Phoenix (Arize)](https://github.com/Arize-ai/phoenix) | Open-source LLM observability; traces agent reasoning steps and tool calls with anomaly detection |
| [AudAgent](https://arxiv.org/abs/2511.07441) | Automated privacy policy compliance auditing via an "auditing automaton" that validates runtime data practices |
| [Invariant Analyzer](https://invariantlabs.ai/) | Security analysis for MCP deployments; detects exfiltration patterns like inbox-fetch→external-send sequences in agent traces |
| [NotFair](https://notfair.co) | Google Ads MCP server for AI agents. Diagnose campaigns, recommend optimizations, execute approved changes via the Google Ads API. |

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
- **[An AI Agent Hacked a Government Site on an Ordinary Task](https://webofmike.com/agent-tried-sql-injection-ordinary-task/)** — Analysis of OpenAI's disclosure that an evaluation agent accessed non-public files on Australia's Medicare statistics portal, and of Transluce's report of agents attempting SQL injection, XSS, path traversal, and command injection during ordinary data-retrieval tasks; covers where Cloudflare blocked the probes and how an unprotected pre-production host was reached instead; September 2026
- **[Check Point: RCE and API Token Exfiltration Through Claude Code Project Files](https://research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files/)** — How repo-level hooks, MCP definitions, and env settings became an attack surface (CVE-2025-59536, CVE-2026-21852); February 2026
- **[Adversa AI: Top AI Coding Agent Security Resources](https://adversa.ai/blog/top-ai-coding-agent-security-resources-october-2026/)** — Monthly roundup of coding-agent vulnerabilities, incidents, and research; October 2026

### Courses, Labs & CTFs

| Resource | Type | Description |
|----------|------|-------------|
| [PromptTrace](https://prompttrace.airedlab.com/) | CTF | 7 injection labs + 15-level Gauntlet CTF; unique Context Trace shows full prompt stack in real-time |
| [Gandalf](https://gandalf.lakera.ai/) | CTF | 8-level prompt injection challenge by Lakera; classic resource for learning defense evasion |
| [FinBot Agentic AI CTF](https://genai.owasp.org/resource/finbot-agentic-ai-capture-the-flag-ctf-application/) | CTF | OWASP's financial services agentic AI CTF with real-world vulnerability scenarios |
| [CrowdStrike AI Unlocked](https://www.crowdstrike.com/en-us/blog/introducing-ai-unlocked-interactive-prompt-injection-challenge/) | CTF | Three-room injection challenges with escalating difficulty |
| [Damn Vulnerable LLM Agent](https://github.com/ReversecLabs/damn-vulnerable-llm-agent) | Lab | LangChain-based ReAct agent with intentionally exploitable injection paths; lets you observe how hijacked thoughts propagate through the agent loop |
| [Damn Vulnerable MCP Server](https://github.com/harishsg993010/damn-vulnerable-MCP-server) | Lab | Deliberately vulnerable MCP server for learning MCP pentesting |
| [vulnerable-mcp-servers-lab](https://github.com/appsecco/vulnerable-mcp-servers-lab) | Lab | Collection of vulnerable MCP servers by Appsecco |
| [Microsoft AI Red Teaming Playground](https://github.com/microsoft/AI-Red-Teaming-Playground-Labs) | Lab | Microsoft's AI red teaming training infrastructure |
| [ai-prompt-ctf](https://github.com/c-goosen/ai-prompt-ctf) | CTF | Targets the full agentic stack: RAG retrieval, function calling, and ReAct loops — covers indirect injection paths most CTFs skip |
| [OWASP WrongSecrets LLM](https://wrongsecrets.herokuapp.com/challenge/32) | Lab | OWASP's LLM security challenge (link may be unavailable) |
| [Google AI Red Team Guide](https://services.google.com/fh/files/blogs/google_ai_red_team_digital_final.pdf) | Guide | Google's walkthrough of hacking AI systems |

### Databases & Trackers

| Resource | Description |
|----------|-------------|
| [AI Incident Database](https://incidentdatabase.ai/) | Community-sourced database of AI failures and harms in deployed systems |
| [AI Agent Incident Register](https://companyscope.io/register) | A numbered public corpus of AI agent incidents, each analysed for the legal duty engaged, who bears liability across the chain (deployer / shared / vendor), and the governance that would have prevented it. Adds a per-incident legal-liability layer that security-side trackers do not; machine-readable JSON feed, CC BY 4.0, archived with a Zenodo DOI. |
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
- **[Anthropic Threat Intelligence Report: September 2026](https://www.anthropic.com/threat-intelligence-report-september-2026)** — Agentic intrusion operations by state-linked and criminal actors observed Dec 2025–Aug 2026
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
