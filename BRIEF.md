# PCBA_FPGA_PMOD_Bridge — Small FPGA Multi-I/O Bridge
## Design brief

Design a small FPGA board that bridges four PMOD-style connectors to USB and SPI. Use an FPGA with enough I/O for four 8-signal headers, include configuration flash, an oscillator, USB connectivity, and all required power rails. The board should be intentionally compact enough that FPGA escape and connector fanout matter. Choose the FPGA family and package yourself and document the power-sequencing assumptions.

## Functional requirements

- All 32 header signals land on FPGA user I/O, usable as input or output; any pin the device constrains is listed as such.
- A pin budget covers those 32 plus flash, oscillator, USB, SPI and programming pins, with the remainder stated.
- Either host interface reaches any header; whether the two run concurrently, and how header ownership resolves, is stated.

## Power rails and sequencing

- Every rail the design needs is listed with voltage, tolerance, worst-case current and origin, header supply included.
- Sequencing assumptions are documented: required order, ramp constraints, whether the design enforces them or relies on stated regulator behaviour, and loss-of-input behaviour. Rails ramp monotonically and are in tolerance before configuration is released.
- The per-header supply limit and the outcome of shorting it are defined; any draw taken from USB stays within the limit for the configuration claimed.

## Configuration, clocking and debug

- Flash holds a complete bitstream for the chosen device, loads it at power-up with no modules fitted and no host intervention, and is writable in system with the board assembled.
- The oscillator meets the tightest of the claimed USB speed grade, the SPI port's maximum rate and any PLL input limit, and lands on a clock-capable pin.
- A programming port, per-rail probe access and observable configuration-done status remain usable with modules attached.

## Connectors and interfaces

- Each header carries 8 signals plus supply and ground, pitch and pin assignment per the Pmod interface specification, so standard modules mate unadapted.
- USB connector type, speed grade and role are declared; the connector is mechanically anchored, its pair routed to that grade, and exposed connectors carry ESD protection.
- The SPI port breaks out clock, data and select with adjacent ground returns, and declares role and signalling voltage.

## Escape, fanout and signal integrity

- The outline follows from connectors, mounting and parts; growing it to relieve routing congestion is not an acceptable remedy.
- Package, escape pattern and layer count are resolved together and are manufacturable at a fabrication class fixed before placement.
- Pins are assigned to minimise crossings; header signals and the USB pair keep a continuous reference plane and a return path at each layer change.

## Open choices

- FPGA family, device and package, recorded with I/O count, bank voltages and configuration modes; layer count and stack-up, settled with the escape strategy.
- How USB is realised: hard block, soft core with external PHY, or external controller — it moves both the pin budget and the flash-programming path.
- Oscillator frequency; SPI port role and signalling voltage; whether header supplies are switched or shared.
