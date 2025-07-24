# Claude Guidelines

This repository will be primarily technical prose, it is unlikely to have a large code component.

When writing, please use a professional, technical tone. Avoid heavy use of emojis. Prefer precise and succinct content.

Refer to the README.md in the root of the repo for details on project objectives, directory structure and security guidelines.

Always consider the security guidelines when performing any task.

Whenever a task alters the structure of the repository, consider updating the README.md too.

Prefer keeping the root README.md a concise "front-page" for the project. Place detailed documentation in the `docs/` directory and then link to it in the README.md.

## Documentation Structure

This repository has two types of documentation:

- **`docs/`** - Human-readable documentation (workflow guides, contributing instructions, etc.)
- **`claude/`** - Claude automation instructions (command specs, templates, implementation details)

When adding documentation:
- Use `docs/` for content intended for human readers
- Use `claude/` for automation specifications and Claude-specific instructions
- Respect the naming convention for files (lowercase with hyphens)

## Claude Automation Guidelines

When performing automation tasks, **always refer to the `claude/` directory first** for:

- Command specifications and syntax
- File templates and directory structures  
- GitHub API integration details
- Error handling procedures
- Workflow automation specifics

### Current Claude Documentation (keep this updated):
- `claude/automation-specs.md` - Complete automation specifications for simulation lifecycle

**Important:** Keep this list updated whenever you add new files to the `claude/` directory. This helps Claude know what documentation is available for reference.

## Terminology

- "Testers" are the people that create simulations, schedule runs, create incidents and help client teams solve problems.
- "Client teams" produce the Ethereum clients. They should be looped in when there is an issue with a particular client. They should help debug and troubleshoot.
- "Researchers" in Ethereum generally refer to specification writers. They are largely irrelevant to this process.