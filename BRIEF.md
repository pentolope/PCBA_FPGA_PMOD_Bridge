# PCBA_FPGA_PMOD_Bridge — Small FPGA Multi-I/O Bridge
## Design brief

Design a small FPGA board that bridges four PMOD-style connectors to USB and SPI. Use an FPGA with enough I/O for four 8-signal headers, include configuration flash, an oscillator, USB connectivity, and all required power rails. The board should be intentionally compact enough that FPGA escape and connector fanout matter. Choose the FPGA family and package yourself and document the power-sequencing assumptions.
