# Lighthouse Node Failed to Follow Chain - Required Two Restarts

## Issue Summary

Lighthouse node `lighthouse-validator-02` failed to properly follow the canonical chain after the network restart. The node appeared to sync initially but remained on a stale chain tip, requiring two additional manual restarts to achieve proper synchronization.

## Timeline

- **15:00:00** - Network restart initiated
- **15:02:14** - Lighthouse node started successfully
- **15:05:22** - Node reported "Synced" status but was following wrong chain
- **15:18:45** - Issue detected during chain validation checks
- **15:19:12** - First manual restart attempted
- **15:21:33** - Node synced to wrong chain again
- **15:22:01** - Second manual restart performed
- **15:24:18** - Node successfully synchronized to canonical chain

## Root Cause Analysis

The node appears to have cached an incorrect chain state from before the shutdown. Upon restart, it prioritized this cached state over peer consensus, leading to following a minority fork.

### Potential Causes
1. **Stale Chain Cache:** Node trusted local chain data over network consensus
2. **Peer Selection Issue:** Initial peer connections may have been to nodes with similar stale state
3. **Fork Choice Bug:** Possible issue in fork choice algorithm when handling long-duration restarts

## Impact Assessment

- **Duration:** 24 minutes of incorrect chain following
- **Validators Affected:** 8 validators on this node produced attestations on wrong chain
- **Network Impact:** Minimal - other nodes maintained canonical chain
- **Data Loss:** None - node eventually synchronized correctly

## Resolution Steps

1. **Immediate:** Manual restart resolved the issue temporarily
2. **Second Restart:** Required to achieve permanent fix
3. **Verification:** Confirmed node was following canonical chain by comparing block hashes with other clients

## Client-Specific Behavior

This issue was observed only on Lighthouse nodes. Other client implementations (Prysm, Teku, Nimbus) successfully synchronized on first restart.

## Recommendations

1. Investigate Lighthouse fork choice algorithm behavior after extended downtime
2. Consider implementing additional chain validation on startup
3. Review peer selection strategy when local chain state is potentially stale
4. Add monitoring alerts for chain divergence detection