# NYPL Engineering AI Guidelines

Welcome to the NYPL Engineering AI Guidelines!

Here at NYPL Digital, we are excited about the potential of AI to enhance our engineering work, but we also recognize the need for clear guidelines to ensure responsible and secure use as a quasi-public institution. This document outlines our principles, approved tools, and policies for using AI in our engineering projects.

## North Stars

These principles are non-negotiable and apply to all AI-assisted engineering work at NYPL.

1. **Use only approved tools.** Engineers must use AI tools exclusively from the [approved list](#approved-tools). Using unapproved tools for Library work is prohibited.
2. **Developers are fully accountable.** Every commit, every agent action, every generated output is the responsibility of the engineer who initiated it.
3. **Never expose secrets.** API keys, credentials, and secrets must never be entered into any AI chat or agent context.

---

## Approved Tools

| Tool                 | Scope                                           | Access                                                                 |
| -------------------- | ----------------------------------------------- | ---------------------------------------------------------------------- |
| GitHub Copilot       | Code generation, inline completion, code review | All engineers                                                          |
| Gemini               | Chat, code assistance                           | All engineers — use your NYPL account                                  |
| Claude / Claude Code | Chat, agentic coding                            | **AI Working Group members only** — reach out to WG members for access |

> New tools not on this list require IT/Digital review before use. Submit a request via ServiceNow.

---

## Policies

### 1. Security

- **Hard rule:** Secrets must never appear in agent context. If your codebase stores API keys in files an agent can read, refactor before using AI agents on that project.
- Prefer technical controls (`.gitignore`, secret scanning, environment injection) over relying on `AGENTS.md` instructions alone to exclude sensitive files.
- AI agents must not be granted access to production systems or authorized to run SSH commands without explicit, reviewed approval.

### 2. Code Review & Accountability

- All AI-generated code must be reviewed before merging, as you would review any human-authored PR.
- Engineers must be able to explain every line of code they commit, regardless of how it was produced. If you cannot explain it, do not commit it.
- Clearly indicate AI assistance in pull requests using the [PR template](./templates/PR_TEMPLATE.md).
- An agent's actions are treated as your own: if an agent breaks something, you own the fix.

### 3. Cost & Usage

- Some models are significantly more expensive than others — use the most capable model appropriate for the task, not the most powerful one available.
- Monitor your own usage. The working group will establish team-level cost baselines as part of the Claude rollout.
- Do not share access credentials or seat licenses with others.

### 4. Configuration & Agent Files

- Place `AGENTS.md` (or equivalent, e.g., `.github/copilot-instructions.md`) in your project root to establish project-specific AI behavior.
- Use the [AGENTS.md template](./templates/AGENTS.md) as a starting point. Customize per project; a one-size-fits-all ruleset is explicitly discouraged.
- AI configuration files should be committed to the repo and treated as part of the project's engineering standards.

### 5. Labeling AI-Generated Work

- Work outputs that are largely AI-generated must be clearly labeled per NYPL policy.
- In code contexts, a PR description note (e.g., "Generated with Copilot, reviewed by [engineer]") satisfies this requirement.

---

## Supporting Documents

> All documents below are currently in progress.

| Document                                                             | Description                                                                                                       |
| -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [AGENTS.md Template](./templates/AGENTS.md)                          | Starter configuration file for AI agents in a project repo                                                        |
| [Prompt Engineering Best Practices](./guides/prompt-engineering.md)  | How to write effective prompts, use TDD with AI, and review generated output                                      |
| [File Exclusion & Secret Scanning Guide](./guides/file-exclusion.md) | How to prevent AI tools from reading sensitive files; recommended `.gitignore` patterns and secret scanning setup |
| [Meta-Governance Policy](./META_GOVERNANCE.md)                       | How the working group reviews tools, updates guidelines, and maintains accountability over time                   |

---

## Questions & Governance

- **Slack:** [#eng-ai-working-group](https://nypl.slack.com/archives/C0AT774CGQP)
- Guidelines are reviewed on a recurring cadence by the working group. Check the changelog for updates.
