# Operating System

This document summarizes recommended Windows distributions and practical observations from empirical testing on a high-performance gaming platform (Ryzen 7 9800X3D + Radeon RX 7900 XT). The guidance below reflects a technical assessment with emphasis on minimizing unnecessary services and telemetry to reduce system overhead and surface area for troubleshooting.

Recommended minimal Windows distributions

1. xOS 11 (23H2)
2. KernelOS 11 (23H2)
3. FSOS 11 (24H2)

These distributions are chosen for their minimal default feature set and active communities focused on performance and privacy. They are intended for advanced users who are comfortable applying post-install configurations and managing updates.

## Context and rationale

The primary objective when selecting an OS for this platform is to remove non-essential processes and telemetry that can introduce variability in latency-sensitive workloads (games and real-time rendering). A minimal "zero-bloat" Windows variant reduces background activity and simplifies performance troubleshooting while preserving compatibility with GPU and system drivers.

## Community resources

For a detailed walkthrough and additional rationale, see the FrameSync Labs presentation: https://www.youtube.com/watch?v=uHjGV1NrO_Y. FrameSync maintains an active community on Discord and provides practical guidance, troubleshooting tips, and periodic builds. FSOS in particular benefits from an engaged maintainer that tracks Windows security updates and patches.

## Observations from empirical testing

Based on controlled comparisons using the same hardware and identical application-level settings (only the OS image was changed):

- Average FPS: observed increase of approximately 2.3–2.5%
- 1% lows: observed increase of approximately 1.0–1.3%
- 0.1% lows: observed increase of approximately 0.7–0.9%

## Interpretation and caveats

These deltas indicate modest improvements in sustained frame rates and 1% low behavior when using a minimal OS image, while the worst-case frametimes (0.1% lows) improved slightly. Practically, this means average frame-rate metrics improve, microstutter at the tail of the distribution can improve in a few scenarios.

## Recommendations

- If you prefer a hands-off approach and need vendor support, use a standard Windows build with careful privacy and performance tuning.
- If you are comfortable with advanced configuration, _**FSOS is recommended**_ for its active maintenance, community support, and focused approach to minimizing bloat.
- Always validate with representative workloads (your target games and workloads) and capture frametime distributions, not just averages. Use tools such as PresentMon, CapFrameX, or an equivalent telemetry tool to measure Average FPS, 1% lows, and 0.1% lows.

## Testing methodology (brief)

- Hardware: refer to `pc-spec.md` for the exact platform configuration.
- Procedure: install OS image, apply standard driver stack, keep application settings constant, and run multiple iterations of representative benchmarks. Aggregate results and report median values for stability.

## Closing notes

Operating system choice can provide measurable, but typically modest, improvements to gaming performance. The OS is rarely the primary bottleneck on a well-provisioned system; prioritize GPU/driver stability, thermal management, and application-level settings first. Use minimal OS images when you require deterministic, low-noise environments for benchmarking or when you prefer a lean system profile for gaming.
