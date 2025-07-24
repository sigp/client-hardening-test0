# Ethereum Client Hardening

This repository contains simulations and analyses of adverse network conditions and attack scenarios targeting Ethereum clients. The goal is to systematically test, document, and improve the resilience of Ethereum client implementations against various forms of network instability and malicious activity.

## Purpose

The Ethereum network's security and stability depend on the robustness of client implementations. By simulating challenging network conditions and attack vectors, we aim to:

- Identify vulnerabilities and edge cases in client behavior
- Document recovery mechanisms and failure modes
- Strengthen the overall resilience of the Ethereum ecosystem

This effort focuses specifically on client implementation resilience and purposely avoids duplicating existing efforts by tracking or documenting protocol-level vulnerabilities or improvements (see [ethereum/consensus-specs](https://github.com/ethereum/consensus-specs)).

## Repository Structure

Each simulation is organized into the following structure:

```
simulations/
├── simulation-name/
│   ├── definition.md           # Simulation specification
│   └── runs/                   # Individual test executions
│       ├── run-001/
│       │   ├── description.md  # Detailed run parameters
│       │   └── incidents/      # Issues discovered during run
│       │       ├── incident-title/
│       │       │   ├── description.md
│       │       │   └── [logs, screenshots, etc.]
│       │       └── another-incident/
│       │           └── ...
│       └── run-002/
│           └── ...
```

### Simulation Components

#### Definition (`definition.md`)
Each simulation begins with a clear specification that includes:
- Objective and scope of the simulation
- High-level description of the adverse condition or attack
- Expected client behaviors and failure modes
- Success criteria and measurement approach

#### Runs (`runs/`)
Individual executions of a simulation, each containing:
- **Description** (`description.md`): Specific parameters including client distribution, network topology, timing, and environmental conditions
- **Incidents** (`incidents/`): Directory containing individual issues discovered during the run, where each incident has its own subdirectory with:
  - Issue description and impact assessment
  - Root cause analysis
  - Resolution steps taken
  - Client-specific behaviors observed
  - Supporting materials (logs, screenshots, network captures, etc.)


## Getting Started

1. Browse existing simulations in the `simulations/` directory
2. Start with the [`example-simulation`](simulations/example-simulation/) to understand the repository structure
3. Review simulation definitions to understand the test scenarios
4. Examine run results to see real-world client behavior under stress
5. Contribute new simulations or run variations of existing ones

## Security

This repository practices responsible disclosure for any bugs or vulnerabilities discovered during simulations. **Do not make public any security issues until the owners or maintainers of the affected software have given explicit permission.** 

When documenting findings:
- Sanitize logs and remove any sensitive information
- Avoid publishing detailed attack vectors or exploits
- Coordinate with client teams before including vulnerability details

## Contributing

When adding new simulations:
- Ensure the simulation specification is detailed enough for reproducibility
- Document all parameters and environmental conditions
- Provide clear analysis of results and findings
- Follow the established directory structure
- Adhere to responsible disclosure practices outlined in the Security section

### Claude Code

This repository is designed to leverage Claude Code for automating repetitive or menial tasks. Contributors are encouraged to:

- Update `CLAUDE.md` when adding new features or aiming to improve the contributing experience
- Use Claude Code to help with file organization, template generation, and documentation tasks
- Ensure all AI-generated content is fully reviewed by the human contributor before submitting a PR

**Important:** We strongly oppose adding verbose, unnecessary "AI slop" to this repository. All content must be concise, technically accurate, and provide genuine value.

#### Human-First Design

The repository should always remain usable **without an LLM**. We should design first for humans, then use LLMs to automate on top of that.

---

*This project supports the ongoing effort to strengthen Ethereum client implementations and improve network resilience against adverse conditions and attacks.*