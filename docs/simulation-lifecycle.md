# Simulation Lifecycle

This document outlines the workflow for creating, executing, and documenting Ethereum client hardening simulations. The process is designed to maximize ease of use while enabling natural collaboration between testers and client teams.

## Overview

The simulation lifecycle consists of three main phases:

1. **Simulation Creation** - One-time setup of the simulation definition
2. **Run Execution** - Individual test runs managed via GitHub PRs
3. **Incident Management** - Collaborative issue resolution via GitHub Issues

## Phase 1: Simulation Creation

Simulations are created once and can be reused for multiple runs. This is typically done by testers defining new test scenarios.

For example, we might create a standard non-finality scenario and the re-run it after big client updates (e.g. hard-fork).

You can create simulations manually by setting up the directory structure and writing the definition, or use Claude commands for assistance:

```bash
claude create a new simulation called "non-finality"
```
## Phase 2: Run Execution

When you want to execute a simulation run, create a GitHub PR that tracks the entire run lifecycle.

### Starting a Run

Create a run either manually or with Claude assistance:

```bash
claude create a run for the non-finality sim called "july-2025"
```

## Phase 3: Incident Management

When issues are discovered during a run, create GitHub Issues for collaborative investigation.

### Creating Incidents

```bash
claude raise an incident that "lighthouse node failed to sync" for the latest run in "non-finality"
```

### Collaboration

- **Client teams** can comment directly on incident issues
- **Testers** share logs, analysis, and findings
- **Issues remain open** until fully understood and documented
- **Large files** can be attached or linked as needed

## Phase 4: Run Completion

When the run finishes, update the PR with final results and merge to preserve the complete history.

```bash
claude complete the latest "non-finality" run. The summary is "Network recovered with 2 incidents discovered"
```

The final summary includes:
- **Key findings** - Main observations and discoveries
- **Incident outcomes** - Status of all issues found
- **Next steps** - Recommended follow-up actions

## Benefits

### For Testers
- **Low friction** - Start runs immediately without bureaucracy
- **Organized** - All run information centralized in one PR
- **Trackable** - Clear progress through checklists

### For Client Teams
- **Natural workflow** - Standard GitHub issue collaboration
- **Focused discussions** - Each incident has dedicated space
- **Complete context** - Full run history available in PR

### For the Project
- **Searchable** - All incidents discoverable via GitHub search
- **Linkable** - Easy cross-referencing between runs and incidents
- **Scalable** - Supports many concurrent runs
- **Transparent** - Complete audit trail of all activities

## Getting Started

1. **Browse existing simulations** in the `simulations/` directory
2. **Review the example simulation** to understand the structure
3. **Start a test run** or create a new simulation
4. **Use Claude commands** to streamline the process

For detailed automation specifications, see the `claude/` directory.