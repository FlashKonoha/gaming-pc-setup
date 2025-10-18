# RAM

Part: `Corsair VENGEANCE RGB 64GB (2 x 32GB) DDR5-6000 PC5-48000 CL30 Dual Channel Desktop Memory Kit CMH64GX5M2M6000Z30 - Gray`

## Summary

This document records observed behaviour and performance characteristics for the referenced DDR5 memory kit and provides practical guidance for selecting, validating, and tuning system memory for low-latency gaming and stability-focused workloads.

## Context

During initial validation the installed modules exhibited instability under stress: failures occurred either immediately or within the first five minutes of extended test runs. Replacing the modules under warranty and applying conservative voltage adjustments restored stable operation for subsequent validation. These results underscore the importance of kit-level validation and coordinated BIOS/firmware configuration when tuning high-speed DDR5 memory.

## Latency calculation (quick reference)

Formula (derived):

Latency (ns) = (CL / Data rate (MT/s)) × 2000

Example (this kit):

Latency (ns) = 30 × 2000 / 6000 = 10.0 ns

Interpretation: each column access requires approximately 10 ns of access time at the specified parameters.

## Comparative latency and observed impact

| Memory Kit     | Speed (MT/s) | CL  | True Latency (ns) | Relative impact (qualitative)                             |
| -------------- | ------------ | --- | ----------------- | --------------------------------------------------------- |
| DDR4-3200 CL16 | 3200         | 16  | 10.0              | Baseline                                                  |
| DDR5-4800 CL40 | 4800         | 40  | 16.7              | Higher latency; more bandwidth                            |
| DDR5-6000 CL30 | 6000         | 30  | 10.0              | Comparable latency to good DDR4 with higher throughput    |
| DDR5-7200 CL34 | 7200         | 34  | 9.4               | Low latency and very high bandwidth — diminishing returns |

In practical gaming workloads, latency differences between reasonably matched kits (for example CL36 vs CL30 at similar data rates) typically translate into single-digit percentage differences in frame-rate metrics; the CPU and GPU subsystem, driver stack, and thermal/power limits often dominate.

## Technical notes and recommendations

- Kit selection: prioritize matched kits purchased as a set (single part number) and reference the motherboard QVL where available.
- Validate out of the box: run MemTest86 or an equivalent memory validation tool at stock settings before enabling XMP/DOCP profiles.
- BIOS coordination: high-speed DDR5 requires correct BIOS settings (memory training, VDD and VDDQ voltages, and timing presets). Apply changes incrementally and document stable profiles.
- XMP/DOCP caution: enabling XMP/DOCP can expose marginal modules. If instability appears, test at JEDEC defaults and raise frequency/timings incrementally.
- Single vs dual-rank: performance and stability can differ by rank configuration; consult vendor documentation and benchmarks for your workload.
- Thermals and placement: ensure adequate airflow around DIMMs; some high-performance modules are sensitive to elevated temperatures.

## Validation workflow

1. Install kit and verify SPD values in BIOS.
2. Boot to OS and run a quick memory check (MemTest86 or Windows Memory Diagnostic) to identify early failures.
3. If passing, enable target profile (XMP/DOCP) and repeat validation under representative workloads (stress test + gaming scenario).
4. If instability occurs, revert to last-known-good settings, test JEDEC defaults, and then tune voltages/timings conservatively.
5. Record stable profiles (export if UEFI supports it) and retain the BIOS image/checksum for reproducibility.

## Theory (brief)

DDR memory transfers data on both the rising and falling edges of the memory clock. Given a data rate in MT/s, the base clock frequency is half the data rate. Converting cycles (CL) to absolute time yields the latency formula above.

Derivation (compact):

Clock frequency (MHz) = Data rate (MT/s) / 2

> Cycle time (ns) = 1000 / Clock frequency (MHz)

> Latency (ns) = CL × Cycle time (ns) = (CL / Data rate (MT/s)) × 2000

## Closing notes

Memory tuning delivers measurable benefits, but it is one component in a larger system. Prioritize reproducible validation, conservative changes, and retaining a rollback plan (known-good BIOS and exported profiles). When in doubt, engage vendor support or the memory/motherboard communities with reproducible logs and test artifacts.
