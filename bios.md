# BIOS

> Motherboard: `ASUS X870E-E ROG Strix Gaming WiFi AMD AM5 ATX Motherboard`

## Summary

This document records BIOS selection, observed stability characteristics, and recommended practices for firmware management on the referenced AM5 platform. The guidance below is intended to help maintain a reproducible, stable baseline for performance testing and daily use. It emphasizes conservative update practices, verification of vendor-supplied images, and a repeatable validation workflow.

## Observed behavior (2025-10-18)

| BIOS Specifications |                                                                    |
| ------------------- | ------------------------------------------------------------------ |
| Version             | 1401                                                               |
| Size                | 16.53 MB                                                           |
| Release Date        | 2025/05/06                                                         |
| SHA-256             | `B9C3212348CB3EC103F1BDF2F8EE533E31DE29FA8CE3253F90C1A5871145617A` |

As of the date above, version 1401 was identified as the most stable baseline for the test platform. An attempted upgrade to version 1715 introduced regressions across memory timing behavior and voltage handling that manifested as system instability and application/driver crashes. The system was returned to 1401 to restore a reproducible baseline for further optimization.

## Diagnosis and technical details

- Symptom set: degraded memory timing stability, intermittent CPU/GPU crashes during stress and gaming workloads, and altered voltage behavior under load.
- Root-cause hypothesis: the newer BIOS contained changes to memory training, power management, or microcode that interacted poorly with this hardware configuration and the tuned firmware/DRAM parameters in use.
- Verification performed: rollback to the previously known-good image (1401) recovered stable operation and restored expected timing/voltage characteristics.

## Recommendations and safe update workflow

1. Maintain a known-good baseline: keep a local copy of the BIOS image and its checksum for the version that is validated on your machine.
2. Review release notes: only consider updating for fixes that address your specific problem domain (e.g., memory training, CPU microcode, or stability patches).
3. Export current settings: where the UEFI supports it, export a BIOS profile before making changes so you can reapply validated settings if the update preserves layouts.
4. Flash with verification: verify downloaded firmware with the vendor-provided checksum (SHA-256) before flashing.
5. Incremental validation: after any firmware change, reinstall drivers where applicable and run a short validation sequence (POST checks, OS boot, a memory test such as MemTest86, and a brief stress scenario representative of your workload).
6. Observe telemetry and logs: review Windows Event Viewer for WHEA or other hardware errors and monitor for driver crash events.
7. Rollback plan: be prepared to revert to the known-good image and reapply settings if regressions appear.

## Testing notes

- Always test firmware updates with the full stack you intend to use: specific driver versions, memory configuration, and power/thermal profiles can all influence stability.
- For memory-related investigations, disable any automatic overclocks or XMP/DOCP profiles, validate SPD values, and run at JEDEC defaults if troubleshooting.
- Capture reproducible failure traces when possible (crash dumps, event logs, and benchmark outputs) to aid in escalation with the vendor or community.

## Settings and risk disclaimer

The configuration and tuning used during these tests are specific to the referenced hardware and workload. BIOS options and voltage/timing adjustments can cause instability or hardware damage if applied incorrectly. The settings documented in this repository are provided for informational purposes only; do not copy them verbatim without understanding their implications and without performing your own validation. Proceed at your own risk.
