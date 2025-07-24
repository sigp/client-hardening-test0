# Claude Automation Specifications

This document contains technical specifications for Claude automation of the simulation lifecycle. This includes command syntax, GitHub API integration, file templates, and workflow automation details.

## Command Specifications

### Simulation Commands

#### Create Simulation
```
claude create simulation "description"
claude create simulation "non-finality over 3 epochs"
```

**Implementation:**
- Create directory: `simulations/{sanitized-name}/runs/`
- Generate `definition.md` from template
- Open GitHub PR for simulation review
- Use labels: `type:simulation`, `status:draft`

**Template: definition.md**
```markdown
# {Simulation Name}

## Objective

{Auto-generated based on description, user can edit}

## Scope

This simulation examines how different Ethereum client implementations handle:
- {Key behavior 1}
- {Key behavior 2}
- {Key behavior 3}

## Simulation Description

### {Phase 1 Name}
{Description}

### {Phase 2 Name}
{Description}

## Expected Client Behaviors

### During {Phase 1}
- {Expected behavior 1}
- {Expected behavior 2}

### During {Phase 2}
- {Expected behavior 1}
- {Expected behavior 2}

## Success Criteria

- {Criterion 1}
- {Criterion 2}
- {Criterion 3}

## Measurement Approach

- {Measurement method 1}
- {Measurement method 2}
```

### Run Commands

#### Start Run
```
claude start run "simulation-name"
claude start run "simulation-name" --duration "2 hours" --clients "lighthouse,prysm"
claude start run "simulation-name" --clients "lighthouse:4,prysm:3,teku:2"
```

**Implementation:**
1. Create branch: `run/{simulation-name}-{YYYY-MM-DD}-{HH-MM}`
2. Create directory: `simulations/{simulation-name}/runs/run-{XXX}/`
3. Generate `description.md` from template
4. Open GitHub PR with run tracking template
5. Use labels: `type:run`, `status:active`, `simulation:{name}`

**Template: Run PR Description**
```markdown
# [RUN] {Simulation Name} - {Brief Description}

## Run Parameters
- **Simulation:** {simulation-name}
- **Duration:** {duration}
- **Start Time:** {planned-start-time}
- **Clients:** 
  - Lighthouse: {count} nodes
  - Prysm: {count} nodes
  - Teku: {count} nodes
  - Nimbus: {count} nodes

## Status Checklist
- [ ] Run parameters defined
- [ ] Infrastructure prepared  
- [ ] Run executed
- [ ] Incidents documented
- [ ] Final summary completed

## Incidents
{Auto-populated as incidents are created}

## Results Summary
*To be completed when run finishes*

---
*This PR tracks the complete lifecycle of this simulation run. Incidents will be created as separate issues and linked here.*
```

**Template: description.md**
```markdown
# Run {XXX}: {Simulation Name} - {Brief Description}

## Run Parameters

**Date:** {YYYY-MM-DD}
**Duration:** {duration}
**Start Time:** {HH:MM UTC}
**End Time:** {HH:MM UTC}

## Network Configuration

### Client Distribution
{Auto-generated based on --clients parameter}

### Infrastructure
- **Total Validators:** {calculated}
- **Network Type:** {testnet/mainnet/custom}
- **Hardware:** {standard specs}
- **Client Versions:**
  - Lighthouse v{version}
  - Prysm v{version}
  - Teku v{version}
  - Nimbus v{version}

## Test Execution

### Procedure
{To be filled during execution}

### Monitoring
{To be filled during execution}

## Expected vs Actual Results

### Expected
{Copy from simulation definition}

### Actual Summary
{To be completed after run}

## Incidents Discovered

See the `incidents/` directory for detailed analysis of issues encountered during this run.
```

#### Complete Run
```
claude complete run --summary "brief summary"
claude complete run --pr 123 --summary "Network recovered successfully with 2 incidents"
```

**Implementation:**
- Update PR description with summary
- Check all checklist items as complete
- Merge PR to preserve run history
- Close any remaining open incidents

### Incident Commands

#### Create Incident
```
claude create incident "description"
claude create incident "lighthouse node failed to sync" --client lighthouse --severity high
claude create incident "prysm sync delay" --client prysm --run-pr 123
```

**Implementation:**
- Create GitHub issue from template
- Link to run PR automatically
- Add labels: `type:incident`, `client:{name}`, `severity:{level}`
- Update run PR checklist with new incident
- Auto-assign client team members based on labels

**Template: Incident Issue**
```markdown
# {Incident Title}

## Incident Summary
{Brief description}

## Run Context
- **Run PR:** #{pr-number}
- **Simulation:** {simulation-name}
- **Time:** {timestamp}
- **Client:** {client-name} v{version}

## Timeline
- {time} - {event}
- {time} - {event}

## Impact
- **Affected validators:** {count}
- **Duration:** {duration}
- **Network impact:** {severity}

## Investigation
*Collaborative space for analysis and findings*

## Resolution
*To be completed when incident is resolved*

---
**Labels:** `type:incident`, `client:{name}`, `severity:{level}`, `run:#{pr}`
```

## GitHub Integration

### Authentication
Requires `gh` CLI authentication:
```bash
gh auth login
```

### API Operations

#### Create Branch
```bash
git checkout -b run/{simulation-name}-{timestamp}
```

#### Create PR
```bash
gh pr create --title "[RUN] {title}" --body "$(cat pr-template.md)" --label "type:run,status:active"
```

#### Create Issue
```bash
gh issue create --title "{title}" --body "$(cat issue-template.md)" --label "type:incident,client:{name}"
```

#### Update PR
```bash
gh pr edit {number} --add-label "status:complete"
```

### Label System

**Types:**
- `type:simulation` - Simulation definition PRs
- `type:run` - Run execution PRs  
- `type:incident` - Incident issues

**Clients:**
- `client:lighthouse`
- `client:prysm` 
- `client:teku`
- `client:nimbus`

**Severity:**
- `severity:low`
- `severity:medium`
- `severity:high`
- `severity:critical`

**Status:**
- `status:draft` - Work in progress
- `status:active` - Currently executing
- `status:investigating` - Under investigation
- `status:complete` - Finished
- `status:resolved` - Issue resolved

## Directory Management

### Simulation Directory Structure
```
simulations/{simulation-name}/
├── definition.md
└── runs/
    ├── run-001/
    │   ├── description.md
    │   └── incidents/
    └── run-002/
        └── ...
```

### Run Numbering
- Auto-increment based on existing runs
- Format: `run-001`, `run-002`, etc.
- Pad with zeros for sorting

### Branch Naming
- Format: `run/{simulation-name}-{YYYY-MM-DD}-{HH-MM}`
- Sanitize simulation names (lowercase, hyphens)
- Use UTC timestamps

## File Templates

### Client Distribution Parsing
Parse `--clients` parameter:
```
"lighthouse:4,prysm:3,teku:2" -> 
- Lighthouse: 4 nodes (44.4%)
- Prysm: 3 nodes (33.3%) 
- Teku: 2 nodes (22.2%)
```

### Timestamp Formatting
- Use ISO 8601 format: `2024-01-15T14:00:00Z`
- Display times in UTC
- Auto-calculate end times based on duration

## Error Handling

### GitHub API Failures
- Retry with exponential backoff
- Provide clear error messages
- Suggest manual fallback steps

### Directory Conflicts
- Check for existing runs before creating
- Suggest alternative names if conflicts exist
- Validate simulation exists before creating runs

### Missing Dependencies
- Verify `gh` CLI is installed and authenticated
- Check git repository status
- Validate required permissions

## Automation Workflows

### GitHub Actions Integration
Potential automations:
- Auto-assign reviewers based on client labels
- Update run PR when incidents are closed
- Generate summary reports for completed runs
- Archive old runs to reduce repo size

### Notification Systems
- Slack/Discord integration for incident creation
- Email notifications for critical incidents
- Status updates for long-running simulations