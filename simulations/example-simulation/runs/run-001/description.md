# Run 001: Complete Network Shutdown - 1 Hour Duration

## Run Parameters

**Date:** 2024-01-15  
**Duration:** Network shutdown for exactly 60 minutes  
**Shutdown Time:** 14:00 UTC  
**Restart Time:** 15:00 UTC  

## Network Configuration

### Client Distribution
- **Lighthouse:** 4 nodes (40% of network)
- **Prysm:** 3 nodes (30% of network) 
- **Teku:** 2 nodes (20% of network)
- **Nimbus:** 1 node (10% of network)

### Infrastructure
- **Total Validators:** 64 (distributed across all clients)
- **Network Type:** Private testnet
- **Genesis Time:** 2024-01-10 12:00 UTC (5 days prior to test)
- **Slot Duration:** 12 seconds
- **Epoch Duration:** 32 slots (6.4 minutes)

### Environmental Conditions
- **OS:** Ubuntu 22.04 LTS on all nodes
- **Hardware:** 4 CPU cores, 8GB RAM, 100GB SSD per node
- **Network:** Gigabit ethernet, <1ms latency between nodes
- **Client Versions:**
  - Lighthouse v4.5.0
  - Prysm v4.1.1
  - Teku v23.12.0
  - Nimbus v23.11.0

## Test Execution

### Shutdown Procedure
1. All nodes terminated simultaneously using `systemctl stop` commands
2. No graceful shutdown period provided
3. Network monitoring confirmed zero active connections at 14:00:05 UTC

### Monitoring During Downtime
- Database files verified as uncorrupted every 15 minutes
- System resources remained stable
- No unexpected process restarts detected

### Restart Procedure
1. All nodes started simultaneously at 15:00 UTC using `systemctl start`
2. Startup logs captured for analysis
3. Network connectivity monitored in real-time

## Expected vs Actual Results

### Expected
- All clients restart within 2 minutes
- Peer connections established within 5 minutes
- Block production resumes within 10 minutes
- Finality achieved within 20 minutes

### Actual Summary
- Most clients restarted successfully within expected timeframes
- Two significant incidents occurred requiring investigation
- Network ultimately recovered but with longer delays than anticipated
- Final state: All nodes synchronized and network operating normally

## Incidents Discovered

See the `incidents/` directory for detailed analysis of issues encountered during this run.