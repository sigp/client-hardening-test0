# Repository Structure

Each simulation is organized into the following structure:

```
simulations/
├── simulation-name/
│   ├── definition.md           # Simulation specification
│   └── runs/                   # Individual test executions
│       ├── 001-july-2025/
│       │   ├── description.md  # Detailed run parameters
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
- **Incidents**: Issues discovered during the run are tracked as GitHub issues with appropriate labels linking them to the specific run

## Example

See the [`example-simulation`](../simulations/example-simulation/) for a complete example of this structure in practice.