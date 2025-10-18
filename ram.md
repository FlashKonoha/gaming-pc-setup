# RAM

Part: `Corsair VENGEANCE RGB 64GB (2 x 32GB) DDR5-6000 PC5-48000 CL30 Dual Channel Desktop Memory Kit CMH64GX5M2M6000Z30 - Gray`

## Context

I initially started optimizing and realized my RAM pretty much couldn't survive any stress tests. It would either fail instantly or within first 5 minutes. I went ahead and swapped the sticks out with Microcenter and then it felt more stable with minor voltage adjustments.

## Latency

> Latency (ns) = CL x 2000 / Data Rate (MHz)

Current hardware results in:

> Latency (ns) = 30 cycles x 2000 / 6000 MT/s = 10ns

This means my current RAM has an actual access latency of ≈10 nanoseconds per column access.

## Importance

Picking hardware for gaming relies on fast response time, heres a comparison of latency calculation for different memory kits

| Memory Kit     | Speed (MT/s) | CL  | True Latency (ns) | Observed Impact                                       |
| -------------- | ------------ | --- | ----------------- | ----------------------------------------------------- |
| DDR4-3200 CL16 | 3200         | 16  | 10.0              | Baseline                                              |
| DDR5-4800 CL40 | 4800         | 40  | 16.7              | Slightly slower responsiveness, higher bandwidth      |
| DDR5-6000 CL30 | 6000         | 30  | 10.0              | Equal latency to good DDR4, but much higher bandwidth |
| DDR5-7200 CL34 | 7200         | 34  | 9.4               | Top-tier latency + bandwidth — diminishing returns    |

FPS gap between a 36CL and a 30CL would barely be 1-2%

## Theory

Memory timings are based on click cycles, but we want time (ns)

DDR memory is double data rate (DDR) -- it transfers data twice per clock cycle.
So the actual clock frequency is half the date rate:

> Clock frequency (MHz) = Data rate (MT/s) / 2

Each clock cycle takes:

> Cycle time (ns) = 1 x 1000 / Clock Frequency (MHz)

because 1MHz = 10⁶ cycles / sec = 1 µs per million cycles = 1000 ns per MHz

Now multiply the cycle time by CL (how many cycles it takes):

> Latency (ns) = CL × Cycle time (ns)

Substitute the cycle time expression:

> Latency (ns) = CL x ( 1000 / Clock Frequency (MHz) )

And since clock frequency = (data rate / 2):

> Latency (ns) = CL x ( 1000 / Data rate (MT/s) / 2 ) = ( CL / Data rate (MT/s) ) x 2000
