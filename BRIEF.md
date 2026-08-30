# PCBA_FPGA_PMOD_Bridge — Small FPGA Multi-I/O Bridge

**Benchmark ID:** 16  
**Difficulty:** 3/5  
**Brief detail:** 2/5  
**Category:** fpga  
**Likely layer count:** 4  
**Primary stressors:** FPGA escape, multiple voltage rails, clock distribution, connector fanout

## Design brief

Design a small FPGA board that bridges four PMOD-style connectors to USB and SPI. Use an FPGA with enough I/O for four 8-signal headers, include configuration flash, an oscillator, USB connectivity, and all required power rails. The board should be intentionally compact enough that FPGA escape and connector fanout matter. Choose the FPGA family and package yourself and document the power-sequencing assumptions.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
