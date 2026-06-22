# AGENTS.md

## Project Overview

[One sentence: language/framework, key versions, what makes this repo architecturally non-standard]

## Tech Stack

- Framework: `[ie. Next.js 15 (App Router + Pages Router hybrid)]`
- Language: `[ie. TypeScript]`
- Package Manager: `[ie. pnpm (always use pnpm, never npm)]`

## Key Commands

- Install: `[command]`
- Dev server: `[command]`
- Run all tests: `[command]`
- Run one test: `[command with path/pattern flag]`
- Lint: `[command]`
- Build/compile: `[command]` _(if applicable)_

## Non-Obvious Patterns

### [Pattern name]

[1–3 sentences explaining the mechanism, not just the rule]

## Code Style

- [Convention or constraint]
- [Convention or constraint]

## Testing Rules

- Write tests for all new functionality.
- [Mocking/stubbing convention for this repo]
- [External service strategy: VCR cassettes / webmock / pytest-httpretty / MSW / etc.]
- Run `[test command]` before marking any task complete.
- Tests must be deterministic and isolated — no order-dependent state.

## Boundaries

### Always fine

- Read files and list directory contents
- Run lint, typecheck, and single test files
- Add or edit tests

### Ask first

- Install or remove dependencies (Gemfile, package.json, requirements.txt)
- Delete files
- Make schema or migration changes
- Open PRs or push to any branch

### Never

- Commit `.env`, secrets, credentials, or API keys
- Force push to `main` or any protected branch
- Modify generated or vendored directories: `vendor/`, `dist/`, `build/`, `node_modules/`, `app/assets/builds/`
- [Any repo-specific protected paths — e.g., Solr config, IIIF schema files]

## Project Structure

- `[path]` — [why it's worth calling out]
- `[path]` — [why it's worth calling out]