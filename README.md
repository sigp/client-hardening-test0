# Ethereum Client Hardening

This repository contains simulations and analyses of adverse network conditions and attack scenarios targeting Ethereum clients. The goal is to systematically test, document, and improve the resilience of Ethereum client implementations against various forms of network instability and malicious activity.

## Purpose

The Ethereum network's security and stability depend on the robustness of client implementations. By simulating challenging network conditions and attack vectors, we aim to:

- Identify vulnerabilities and edge cases in client behavior
- Document recovery mechanisms and failure modes
- Strengthen the overall resilience of the Ethereum ecosystem

This effort focuses specifically on client implementation resilience and purposely avoids duplicating existing efforts by tracking or documenting protocol-level vulnerabilities or improvements (see [ethereum/consensus-specs](https://github.com/ethereum/consensus-specs)).

## Contributing

This repository is designed for use with Claude Code. Claude will help you automate and perform menial tasks. For example:

- `claude create a new simulation called "non-finality"`
- `claude create a run for the non-finality sim called "july-2025"`
- `claude raise an incident that "lighthouse node failed to sync" for the latest run in "non-finality"`
- `claude complete the july-2025 non-finality run. the overview is that it went well; we had one issue where lighthouse failed to sync, the lighthouse team fixed it in a PR`

## Documentation

For detailed information about this project:

- **[Repository Structure](docs/repository-structure.md)** - Directory organization and file structure
- **[Simulation Lifecycle](docs/simulation-lifecycle.md)** - Workflow for creating and running simulations

## Security

This repository practices responsible disclosure for any bugs or vulnerabilities discovered during simulations. **Do not make public any security issues until the owners or maintainers of the affected software have given explicit permission.** 

When documenting findings:
- Sanitize logs and remove any sensitive information
- Avoid publishing detailed attack vectors or exploits
- Coordinate with client teams before including vulnerability details

### Claude Code Details

This repository is designed to leverage Claude Code for automating repetitive or menial tasks. Instructions for Claude to reference are found in [CLAUDE.md](./CLAUDE.md) and [claude/](./claude/). Contributors are encouraged to:

- Update [`CLAUDE.md`](./CLAUDE.md) and [`claude/`](./claude/) when adding new features or aiming to improve the contributing experience
- Use Claude Code to help with file organization, template generation, and documentation tasks
- Ensure all AI-generated content is fully reviewed by the human contributor before submitting a PR

**Important:** We strongly oppose adding verbose, unnecessary "AI slop" to this repository. All content must be concise, technically accurate, and provide genuine value.

#### Human-First Design

The repository should always remain usable **without an LLM**.

---

*This project supports the ongoing effort to strengthen Ethereum client implementations and improve network resilience against adverse conditions and attacks.*