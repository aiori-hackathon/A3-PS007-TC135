# A3-PS007-TC135: Privacy-Aware IPv6 Security Monitoring for IoT Devices under Address Rotation

**AIORI Hackathon 3** · Team **KMK** · RV College of Engineering (RVCE), Bengaluru

## Demo Video

[![Watch the demo](https://img.shields.io/badge/YouTube-Watch%20the%20Demo-red?logo=youtube)]([INSERT_YOUTUBE_LINK_HERE](https://youtu.be/G-szpOLln-s))

**Video link:** [https://youtu.be/G-szpOLln-s](https://youtu.be/G-szpOLln-s)

## Team

| Name | Role |
|------|------|
| Kavin Krishnan C | Hardware implementation, verification, testing and software simulations |
| Krupanka R | Software application, AI system integration, algorithms in hardware |

**Mentor:** Dr. Manonmani S, Associate Professor, Department of CSE, RVCE

**Contact:** kavinkrishnanc.cs24@rvce.edu.in

## Problem Statement

**PS007: Privacy-aware IPv6 security monitoring for IoT devices under address rotation.**

IPv6 devices rotate their addresses (privacy extensions, ISP prefix changes). On a static network, a snooper or compromised device is easy to spot from per-address bandwidth or throughput. On a dynamic network, where the address keeps rotating, the attacker's identity effectively changes every cycle, so per-address logs, blocklists and rate limits stop working. Monitoring must also stay privacy-aware: no payload inspection and no permanent tracking of innocent users.

## Our Solution

**Map behaviour, not the address.** Instead of tying an identity to an IPv6 address, we learn a behavioural profile of each device and link every new address back to that profile. We keep the history of those links on a blockchain ledger.

1. **Capture and feature extraction:** open-source tools (e.g. tcpdump, Zeek) measure per-flow bandwidth and throughput in time windows. Only metadata is kept (packet sizes, inter-arrival times, up/down ratio, protocol and port mix, duty cycle). No payloads.
2. **AI behaviour model:** a model trained dynamically on these windows turns each device's activity into a behaviour fingerprint.
3. **Identity resolution:** when a new address appears, its first windows are compared with known profiles. A close match links the address to that profile; otherwise a new profile is created. Profile IDs are pseudonymous hashes.
4. **Blockchain ledger:** each link (profile ID, address, timestamp, fingerprint digest) is appended to a permissioned ledger, giving a tamper-evident history of one profile across all its address rotations.
5. **Anomaly detection and alerts:** alerts fire when a profile drifts from its own baseline, whichever address it is using.

The tracking and verification logic is also targeted at an edge (hardware) node.

## Key Optimizations

| Aspect | Before (IP-keyed) | After (behaviour + ledger) |
|--------|-------------------|----------------------------|
| Identity key | IPv6 address | Behavioural profile ID |
| Tracking across rotation | Lost at every cycle | Continuous via fingerprint matching |
| Detection baseline | Static throughput thresholds | Adaptive per-profile baselines |
| Evidence integrity | Mutable local logs | Append-only, tamper-evident ledger |
| User privacy | Raw IPs and traffic logs | Metadata only, pseudonymous hashed IDs |
| Compute placement | Central collector | Lightweight inference at the edge |

## Evaluation Metrics

- Re-identification accuracy across address rotations
- False-alarm rate
- Detection latency
- Ledger write overhead

## Repository Structure

```
TODO: add the folder layout once the code is uploaded
```

## Setup and Usage

```
TODO: add prerequisites, install steps and run commands
```

## Presentation

The slide deck (PDF) is included in this repository: `A3-PS007-TC135_KMK_AIORI3.pdf`

## References

1. F. Gont, S. Krishnan, T. Narten, R. Draves. *Temporary Address Extensions for Stateless Address Autoconfiguration in IPv6.* RFC 8981, IETF, 2021.
2. F. Gont. *A Method for Generating Semantically Opaque Interface Identifiers with IPv6 SLAAC.* RFC 7217, IETF, 2014.
3. A. Sivanathan et al. "Classifying IoT Devices in Smart Environments Using Network Traffic Characteristics." *IEEE Transactions on Mobile Computing*, 18(8), 2019.
4. E. Rye, R. Beverly, kc claffy. "Follow the Scent: Defeating IPv6 Prefix Rotation Privacy." *ACM IMC*, 2021.
5. S. Nakamoto. *Bitcoin: A Peer-to-Peer Electronic Cash System.* 2008.
6. E. Androulaki et al. "Hyperledger Fabric: A Distributed Operating System for Permissioned Blockchains." *EuroSys*, 2018.
