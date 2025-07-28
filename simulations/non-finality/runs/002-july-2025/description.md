# non-finality - 002-july-2025

## Run Parameters

- **Simulation:** non-finality
- **Start Time:** July 2025
- **Clients:** Mainnet-like distribution (EL: Geth 63%, Nethermind 22%, Besu 10%, Erigon 5%; CL: Prysm 42%, Lighthouse 28%, Teku 21%, Nimbus 9%)

## Network Configuration

### Client Distribution
**Execution Layer:**
- Geth: 63%
- Nethermind: 22% 
- Besu: 10%
- Erigon: 5%

**Consensus Layer:**
- Prysm: 42%
- Lighthouse: 28%
- Teku: 21%
- Nimbus: 9%

### Infrastructure
- **Total Validators:** TBD (based on network size requirements)
- **Network Type:** Testnet
- **Hardware:** 6-core AMD Ryzen boxes, 64GB RAM per node
- **Client Versions:**
  - Geth v1.15.11
  - Nethermind v1.29.2
  - Besu v25.3.0
  - Erigon v3.0.0-alpha5
  - Prysm v6.0.3
  - Lighthouse v7.0.1
  - Teku v25.4.1
  - Nimbus v25.4.1

## Test Execution

### Procedure
1. **Day 1-2:** Run network normally with full validator set
2. **Day 3-9:** Turn off 2/3rds of validators to simulate non-finality conditions
3. **Day 10+:** Turn validators back on and monitor network recovery

### Monitoring
- Manual monitoring via Grafana dashboards (links TBC)
- Network finality status tracking
- Client performance metrics during non-finality period
- Recovery time measurement

## Expected vs Actual Results

### Expected
This simulation examines how different Ethereum client implementations handle:
- Extended periods without finalization (1 week)
- Client behavior under reduced validator participation
- Network recovery mechanisms when validators return
- Performance differences across mainnet-representative client distribution

### Actual Summary
To be completed after run

## Incidents Discovered

[Issues tagged with incident:non-finality:002-july-2025](https://github.com/sigp/client-hardening-test0/issues?q=label%3Aincident%3Anon-finality%3A002-july-2025)