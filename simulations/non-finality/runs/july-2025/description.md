# non-finality - july-2025

## Run Parameters

- **Simulation:** non-finality
- **Start Time:** July 2025
- **Clients:** TBD

## Network Configuration

### Client Distribution
To be determined based on clients parameter

### Infrastructure
- **Total Validators:** TBD
- **Network Type:** TBD
- **Hardware:** TBD
- **Client Versions:**
  - TBD

## Test Execution

### Procedure
To be filled during execution

### Monitoring
To be filled during execution

## Expected vs Actual Results

### Expected
This simulation examines how different Ethereum client implementations handle:
- Extended periods without finalization
- Chain reorganizations during non-finality
- Recovery mechanisms when finality resumes

### Actual Summary
The simulation ran successfully overall. Client implementations demonstrated good resilience during extended non-finality periods. One minor issue was identified where Lighthouse failed to sync, but this was quickly resolved by the Lighthouse team with a bug fix.

## Incidents Discovered

[Issues tagged with incident:non-finality:july-2025](https://github.com/sigp/client-hardening-test0/issues?q=label%3Aincident%3Anon-finality%3Ajuly-2025)

- **Issue #4:** Lighthouse node failed to sync - resolved by Lighthouse team with minor bug fix