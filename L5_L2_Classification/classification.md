# L5 Narrow / L2 General Classification — L_TIMEFLUX
**Platform:** Anticloud | **Tier:** TIER_7_BIOSIGNALS_NEURO | **PAX:** 27B
**IP:** USPTO pending 2026, Anticloud FZ LLE, 0-1.gg | **License:** Apache-2.0

## L5 Narrow
L_TIMEFLUX provides the complete deployment stack for a real-time Anticloud BCI system: containerized TimeFlux graph, Redis broker, PAX 27B real-time alerting, and AIOSS chain audit trail. Narrow scope: clinical real-time BCI deployment.

## L2 General
L2 General: L_TIMEFLUX is the production real-time BCI layer for any TIER_7 clinical deployment. The same TimeFlux stack supports neurofeedback (consumer) and closed-loop neurostimulation (clinical).

## PAX 27B Integration
PAX 27B runs as a TimeFlux node: consuming processed EEG features and generating real-time clinical alerts that are AIOSS-chained for post-hoc audit.

## AIOSS Audit Chain
Every BCI session (session hash + event log hash + PAX alert log hash + stimulation event log hash) is chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Offline-verifiable, tamper-evident, zero cloud dependency.

## Regulatory / Compliance
IEC 62304 (real-time medical software). IEC 60601-2-26 (EEG systems). EU MDR.
