# Requirements — Small FPGA Multi-I/O Bridge

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `d83d5909ac51f392234e833853a1ffec0276ae79a6ab19266e9302e75ae3a2ed`.

## Fixed by the brief

### REQ-01 — The board is a small FPGA board whose function is to bridge four PMOD-style connectors to USB and to SPI.

Brief text:

> Design a small FPGA board that bridges four PMOD-style connectors to USB and SPI.

### REQ-02 — There are four PMOD-style headers of eight signals each, and the FPGA selected must have enough I/O to serve all four.

Brief text:

> Use an FPGA with enough I/O for four 8-signal headers

### REQ-03 — The board includes configuration flash.

Brief text:

> include configuration flash, an oscillator, USB connectivity, and all required power rails

### REQ-04 — The board includes an oscillator.

Brief text:

> an oscillator, USB connectivity, and all required power rails

### REQ-05 — The board includes USB connectivity.

Brief text:

> an oscillator, USB connectivity, and all required power rails

### REQ-06 — The board provides all power rails the design requires.

Brief text:

> an oscillator, USB connectivity, and all required power rails

### REQ-07 — The board is intentionally compact — compact enough that FPGA escape and connector fanout matter.

Brief text:

> The board should be intentionally compact enough that FPGA escape and connector fanout matter.

### REQ-08 — The FPGA family and package are chosen by the design agent as part of this work; they are not supplied by the customer and may not be treated as a given.

Brief text:

> Choose the FPGA family and package yourself

### REQ-09 — The power-sequencing assumptions are documented as a deliverable of the design.

Brief text:

> Choose the FPGA family and package yourself and document the power-sequencing assumptions.

### REQ-10 — Stated requirements are authoritative; open choices are to be made and documented as engineering decisions, not resolved by inventing hidden user requirements.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements.

### REQ-11 — This repository stays a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic does not accumulate in the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

### REQ-12 — The board has an SPI interface: SPI is the second named endpoint of the bridge, so the interface itself must exist, even though its role, signal count, rate and physical interface are left open.

Brief text:

> Design a small FPGA board that bridges four PMOD-style connectors to USB and SPI.

## Open — the design agent decides

### OPEN-01 — Which FPGA family, device and package, and how many usable I/O, banks and clock-capable pins that device provides.

The brief explicitly hands this choice to the designer and names no vendor, family, density or package.

*Decision:* **not yet made.**

### OPEN-02 — How USB connectivity is implemented — inside the FPGA, via a separate interface device, or otherwise — and which USB speed class and role the board presents.

The brief requires 'USB connectivity' and says nothing about speed, role, or which device terminates the link.

*Decision:* **not yet made.**

### OPEN-03 — USB connector type, orientation and placement on the board.

The brief names no connector and gives no mechanical interface requirements.

*Decision:* **not yet made.**

### OPEN-04 — The SPI side of the bridge: whether the board is SPI host or peripheral, how many chip selects and signals, clock rate, and whether SPI appears on a dedicated connector, on a header, or on one of the PMOD sites.

The brief lists SPI as a bridge endpoint, which fixes that the interface exists, but fixes no role, rate, pin count or physical interface for it.

*Decision:* **not yet made.**

### OPEN-05 — Number of supply rails, their voltages, the input power source (bus-powered from USB versus an external input), and regulator topology for each rail — switching, linear or a mix.

The brief requires 'all required power rails' but the rail set follows from the FPGA choice, which is itself open; no voltage, input source or topology is stated.

*Decision:* **not yet made.**

### OPEN-06 — The power-sequencing mechanism — dedicated sequencer, enable chaining, ordered soft-start, or supervisor — plus any power-good monitoring and reset release scheme.

The brief requires the sequencing assumptions to be documented but prescribes no mechanism or ordering.

*Decision:* **not yet made.**

### OPEN-07 — Oscillator type, frequency, output standard and supply, whether more than one clock source is fitted, and how much of the clocking is done in on-chip PLL/MMCM resources.

The brief requires 'an oscillator' and states no frequency, accuracy, jitter budget or output type.

*Decision:* **not yet made.**

### OPEN-08 — Clock distribution topology: which pin the oscillator enters, whether any clock is exported to or imported from the PMOD sites or the SPI interface, and what termination and return-path treatment those nets get.

The brief is silent on clock distribution; it appears only as a benchmark stressor, not as a stated topology.

*Decision:* **not yet made.**

### OPEN-09 — Configuration flash device type, interface width and configuration mode, and whether a programming/debug interface (and what kind) is brought out.

The brief requires configuration flash but names no device, interface, size or programming path.

*Decision:* **not yet made.**

### OPEN-10 — PMOD site definition: connector style and pitch, total pin count per site, whether power and ground pins are provided, at what voltage and current, and the ordering of the eight signals.

The brief says 'PMOD-style' and fixes only the eight signals per site; it does not state a pinout, connector, pitch or supply provision.

*Decision:* **not yet made.**

### OPEN-11 — I/O bank voltage assignment for the header signals and whether any level translation or buffering sits between the FPGA and the connectors.

The brief states no interface voltage, logic standard or translation requirement for the headers.

*Decision:* **not yet made.**

### OPEN-12 — Board outline, actual dimensions, mounting holes, connector keepouts, where each connector sits on the outline, and any enclosure or stacking assumption.

The brief asks for a compact board but gives no dimension, aspect ratio, mounting, placement or mechanical envelope.

*Decision:* **not yet made.**

### OPEN-13 — The layer count and the stackup built on it: whether the four layers metadata calls likely are what the chosen package escape and the rails actually need, plus layer roles, dielectric thicknesses, copper weights, and whether any impedance is controlled and to what target.

Only a likely layer count comes from metadata; the brief states no layer count, stackup, dielectric, impedance or controlled-impedance requirement.

*Decision:* **not yet made.**

### OPEN-14 — FPGA escape strategy: via type (through-hole, via-in-pad, microvia), fanout pattern, minimum trace/space class, and which fabricator's rules that strategy is checked against.

The brief names the escape problem as a stressor but prescribes no package, pitch, via technology or fab process.

*Decision:* **not yet made.**

### OPEN-15 — Whether the externally exposed header, USB and SPI pins get ESD, overvoltage or series protection, and of what kind.

The brief does not mention protection at all; the exposure follows from having external connectors, not from a stated requirement.

*Decision:* **not yet made.**

### OPEN-16 — Any user-facing extras — indicator LEDs, reset or configuration buttons, DIP/strap options, test points — and whether they exist at all.

The brief lists no indicators, controls or test features.

*Decision:* **not yet made.**

### OPEN-17 — Decoupling scheme and PDN impedance targets per rail, and how they are verified.

The brief states no PDN, ripple or decoupling requirement; the targets follow from the still-unchosen FPGA.

*Decision:* **not yet made.**

### OPEN-18 — Fabricator and assembler, and the process capability class (minimum trace/space, annular ring, fine-pitch placement) the design commits to.

The brief names no vendor, process or capability limit.

*Decision:* **not yet made.**

### OPEN-19 — Bring-up and test strategy: what is probed, what is programmed first, whether a test/debug connector exists, and how the four PMOD sites are exercised.

The brief states no test, validation or bring-up requirement.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json). **That file is the authoritative
   record**, and the only one the benchmark's scripts read: a decision written
   only in prose is invisible to `board_status.py` and to any result that
   counts how many decisions an attempt actually made.
2. Answer it under its `OPEN-nn` heading here as well, with the reasoning and
   the evidence that made the choice. This file is the readable copy; where the
   two disagree, the JSON is what happened.
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Asserting that the chosen package escapes cleanly at the design's layer count without ever opening the real pin/ball map and checking the fanout against a specific fabricator's trace/space, drill and annular-ring limits.
- Treating metadata's likely four layers as a fixed requirement, so the layer count and stackup are never justified against the chosen package's escape needs or the rail distribution.
- Claiming 'all required power rails' are present without enumerating the chosen FPGA's actual rail list, tolerances and currents from its datasheet.
- Writing the power-sequencing assumptions as prose while the regulators as drawn have no enable chain, sequencer or monitoring that could enforce the stated order — the brief demands the documentation, so this is the easiest place to fake compliance.
- Inventing header specifics the brief never states: a pin count beyond the eight signals, a supply voltage on the sites, a logic standard, or a named connector part.
- Declaring a board size that sounds compact without a placement that actually holds four header sites, USB, the FPGA escape area and the regulators with legal keepouts.
- Treating 'clock distribution' as solved by placing one oscillator, without checking that its pin is clock-capable for the intended fabric resources and that any exported clock has a real return path.
- Pushing board-specific fixups into the shared PCBA_AutoDesignAndTest toolkit instead of keeping them as configuration in this repository.
