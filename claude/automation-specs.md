# Claude Automation Specifications

This document contains technical specifications for Claude automation of the simulation lifecycle. This includes command syntax, GitHub API integration, file templates, and workflow automation details.

## Command Specifications

### Simulation Commands

#### Create Simulation

When the user requests to create a new simulation, collect the following information:

- `simulation-name`: a name for the simulation. Sanitize it to camel-case.
- `description`: a brief description of the simulation.

You can infer this info from their prompt or ask for it directly.

**Implementation:**
- Create directory: `simulations/{simulation-name}/runs/`
- Generate `definition.md` from template with reference to `description`.
- Open GitHub PR for simulation review
- Use labels: `type:simulation`, `simulation:{simulation-name}`

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
```

### Run Commands

#### Start Run

When the user requests to create a new simulation, collect the following information:

- `simulation-name`: The simulation to run, must match an existing simulation. If it doesn't, give the user a list of existing simulations or an option to create it.
- `run-name`: a name for the run. Suggest something human readable and descriptive related to the date (e.g. "july-2025") or the reason (e.g. "post-pectra-july-2025").  See the "Run Numbering" section below for how you should format the run name.
- `clients`: a list of clients to be involved in the run. This can be execution and consensus clients.
- `start-date`: a loose date as to when the run should start (e.g. can be a specific day or a month, anything is fine).
- `additional-details`: anything else they'd like to provide. E.g., client weightings, client pairs, specific network conditions, time interval, etc.

You can infer this info from their prompt or ask for it directly.

**Implementation:**
1. Create branch: `run/{simulation-name}-{run-name}`
2. Create directory: `simulations/{simulation-name}/runs/{run-name}/`
3. Generate `description.md` from provided information
4. Open GitHub PR with run tracking template
5. Use labels: `type:run`, `run:{simulation-name}:{run-name}`

**Template: Run PR Description**
```markdown
# {simulation-name}: Run {run-name}

## Run Parameters
- **Simulation:** {simulation-name}
- **Start Time:** {start-date}
- **Clients:** : {clients}

## Status Checklist
- [ ] Run parameters defined
- [ ] Infrastructure prepared  
- [ ] Run executed
- [ ] Incidents documented
- [ ] Final summary completed

## Incidents

{Github link to issues with the tag: `issue:{simulation-name}:{run-name}`}

## Resources

*Provide links for block explorers, metrics, etc*

## Results Summary
*To be completed when run finishes*
```

**Template: description.md**
```markdown
# {simulation-name} - {run-name}

## Run Parameters

- **Simulation:** {simulation-name}
- **Start Time:** {start-date}
- **Clients:** : {clients}

## Network Configuration

### Client Distribution
{Auto-generated based on clients parameter}

### Infrastructure
- **Total Validators:** {calculated}
- **Network Type:** {testnet/mainnet/custom}
- **Hardware:** {standard specs}
- **Client Versions:**
  - Lighthouse v{version}
  - Prysm v{version}
  - etc.

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

{Github link to issues with the tag: `issue:{simulation-name}:{run-name}`}
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

See ./docs/repository-structure.md

### Run Numbering
- Auto-increment based on existing runs
- Format: `000-{run-name}`, `001-{run-name}`, etc.
- Pad with zeros for sorting

### Branch Naming
- Format: `run/{simulation-name}-{run-name}`
- Sanitize simulation names (camel-case)

## File Templates

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