# Repository Structure

Each simulation is organized into the following structure:

```
simulations/
├── simulation-name/
│   ├── definition.md           # Simulation specification
│   └── runs/                   # Individual test executions
│       ├── 001-july-2025/
│       │   ├── description.md  # Detailed run parameters
│       │   └── incidents/      # Issues discovered during run
│       │       ├── incident-title/
│       │       │   ├── description.md
│       │       │   └── [logs, screenshots, etc.]
│       │       └── another-incident/
│       │           └── ...
│       └── 002-august-2025/
│           └── ...
```

## Simulation Components

### Definition (`definition.md`)
Each simulation begins with a clear specification that includes:
- Objective and scope of the simulation
- High-level description of the adverse condition or attack
- Expected client behaviors and failure modes
- Success criteria and measurement approach

### Runs (`runs/`)
Individual executions of a simulation, each containing:
- **Description** (`description.md`): Specific parameters including client distribution, network topology, timing, and environmental conditions
- **Incidents** (`incidents/`): Directory containing individual issues discovered during the run, where each incident has its own subdirectory with:
  - Issue description and impact assessment
  - Root cause analysis
  - Resolution steps taken
  - Client-specific behaviors observed
  - Supporting materials (logs, screenshots, network captures, etc.)

## Example

See the [`example-simulation`](../simulations/example-simulation/) for a complete example of this structure in practice.