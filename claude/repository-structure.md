# Repository Structure - Claude Reference

For the human-readable repository structure documentation, see: [docs/repository-structure.md](../docs/repository-structure.md)

This document contains Claude-specific notes about the repository structure for automation purposes.

## Directory Structure for Automation

When creating simulations and runs, follow this exact structure:

```
simulations/
├── {simulation-name}/
│   ├── definition.md
│   └── runs/
│       └── run-{XXX}/
│           ├── description.md
│           └── incidents/
│               └── {incident-slug}/
│                   ├── description.md
│                   └── [supporting files]
```

## Naming Conventions

### Simulation Names
- Convert to lowercase with hyphens: "Non-finality over 3 epochs" → "non-finality-over-3-epochs"
- Remove special characters and spaces
- Keep descriptive but concise

### Run Directories
- Format: `run-001`, `run-002`, etc.
- Zero-pad to 3 digits for proper sorting
- Auto-increment based on existing runs

### Incident Directories
- Convert incident titles to slugs: "Lighthouse restart issue" → "lighthouse-restart-issue" 
- Use lowercase with hyphens
- Keep under 50 characters if possible

## File Templates

### Simulation definition.md
Template location: In automation-specs.md under "Template: definition.md"

### Run description.md  
Template location: In automation-specs.md under "Template: description.md"

### Incident description.md
Template location: In automation-specs.md under "Template: Incident Issue"

## Directory Creation Commands

```bash
# Create simulation
mkdir -p simulations/{simulation-name}/runs

# Create run
mkdir -p simulations/{simulation-name}/runs/run-{XXX}/incidents

# Create incident
mkdir -p simulations/{simulation-name}/runs/run-{XXX}/incidents/{incident-slug}
```

## Validation Rules

Before creating directories:
1. Check if simulation exists
2. Determine next run number by listing existing runs
3. Validate incident slug doesn't conflict with existing incidents
4. Ensure all parent directories exist