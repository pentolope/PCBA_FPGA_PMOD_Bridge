# Architecture — Small FPGA Multi-I/O Bridge

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- FPGA escape
- multiple voltage rails
- clock distribution
- connector fanout

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## FPGA selection and I/O budget

- Which FPGA family, device and package is chosen, and what specifically drives that choice — I/O count, package style and pitch, price, toolchain, or rail simplicity?
- How many usable user I/O does the chosen device provide after configuration, clock and dedicated pins are reserved, and how does that compare with the 32 header signals plus USB, SPI and flash?
- How many I/O banks does the device have, and which banks are the four header sites, the SPI interface and the configuration flash assigned to?
- Does the package style and pitch fit the fabricator capability assumed elsewhere in this document, or does it force a finer class?
- What is the device's junction temperature and power budget under the intended workload, and does the package need any thermal provision on a compact board?

## FPGA escape and fanout

- What escape strategy suits the chosen package — for an area-array package, dog-bone fanout, via-in-pad, microvia or a mix; for a leaded or QFN package, escape directly from the pads — and on which layers do signals leave the device?
- How many signal layers does the stackup leave for the escape once power and ground are accounted for, and does the escape fit in them at the layer count the design commits to?
- What minimum trace width, spacing, drill and annular ring does the escape require, and which fabricator's published capability page confirms those numbers?
- Which pins are deliberately left unconnected to make the escape routable, and does that still satisfy the I/O budget above?
- How do the escape routes reach the four header sites without crossing the clock or USB nets in a way that breaks their return paths?

## Power rails and sequencing

- What is the complete rail list for the chosen FPGA plus the flash, oscillator, any USB stage and any header supply, with each rail's voltage, tolerance and worst-case current?
- Where does input power come from — the USB connection, an external input, or both — and how is contention between sources handled?
- What regulator topology serves each rail, and what evidence supports the thermal and dropout margin for each in the board's compact area?
- What sequencing order does the FPGA datasheet require, what mechanism enforces it, and what are the documented assumptions where the datasheet leaves latitude?
- How is power-good detected and how does it gate reset release and configuration start?
- What happens on brownout, on hot-plug of a PMOD module, and on loss of USB VBUS mid-operation — both if a rail is derived from it and if none is?

## Clock generation and distribution

- What frequency, output standard, accuracy and jitter does the oscillator provide, and what requirement in the design sets those numbers?
- Which FPGA pin does the oscillator drive, and is that pin clock-capable for the resources the design intends to use?
- How many derived clock domains exist inside the FPGA, and are they produced by on-chip PLL/MMCM or by additional external sources?
- Is any clock exported to a PMOD site or to the SPI interface, and if so how is it terminated and what is its return path across the stackup?
- What crossings exist between the USB, SPI and header clock domains, and where are they synchronised?
- How is the oscillator supply decoupled and isolated from the other rails and whatever regulators produce them on a board this small?

## PMOD-style connector fanout

- What connector style, pitch and total pin count defines a site, and what pinout is assigned to the eight signals?
- Do the sites provide power and ground to attached modules, at what voltage and what current limit, and how is that budgeted against the input source?
- At what I/O voltage do the headers run, and is that set directly by an FPGA bank voltage or by translation?
- How are the four sites placed on the outline so that attached modules do not collide with each other, with USB, or with any mounting hardware the design adds?
- What is the length and layer path for each of the 32 signals, and are the four sites treated symmetrically?
- Is any site's signal set constrained to be differential-capable or matched, and if so how is that guaranteed by the pin assignment?

## USB interface

- Is USB implemented in the FPGA fabric, by a dedicated interface device, or through the configuration/debug path, and what is the resulting speed class and role?
- What connector is used, where does it sit on the outline, and what mechanical retention does it need?
- What differential impedance target applies to the USB pair, and what stackup — at the layer count the design commits to — produces it?
- What length, matching and via-count limits does the chosen USB speed impose, and are they met by the routing plan?
- How is the USB pair kept away from the header fanout and the clock nets in the available area?
- If the board is bus-powered, what is the enumerated current draw and does the rail budget stay inside it?

## SPI interface and bridge behaviour

- Is the board the SPI host or the SPI peripheral, and what does the bridge actually move between USB, SPI and the header signals?
- How many SPI signals and chip selects are exposed, at what clock rate, and on what physical connector?
- What logic voltage does the SPI interface use, and does it match the header voltage or need its own bank or translation?
- Does the SPI interface share pins or a bank with the configuration flash, and if so how are the two arbitrated?
- What buffering or flow control exists inside the FPGA between the USB side and the SPI and header sides?

## Configuration and programming

- Which configuration mode does the design use, and what flash device type, interface width and capacity does that mode require for the chosen device?
- What is the flash's supply voltage and does it match the FPGA's configuration bank voltage without translation?
- How is the flash programmed in production and in the lab — through a dedicated header, over USB, or through the FPGA — and is that path exposed on the board?
- What are the configuration timing and pin-state requirements during power-up, and how do they interact with the sequencing scheme above?
- Are the configuration pins shared with user I/O after configuration, and what does that constrain?

## Stackup, impedance and manufacturability

- How many layers does the design actually need, and why — metadata offers four as the likely count, but what do the escape, the rail distribution and any controlled-impedance nets require?
- What are the layer roles, dielectric thicknesses and copper weights, and which fabricator's published stackup are they taken from?
- Which nets, if any, are impedance-controlled, to what target, and what trace geometry achieves it in that stackup?
- How are the power rails distributed across the copper layers, and does any fast or clock net cross a plane split or a gap in its return path?
- What is the minimum feature set (trace/space, drill, annular ring, solder mask sliver) the design needs, and does the assumed fabricator support it at standard cost?
- What assembly constraints — package type, fine-pitch placement, double-sided assembly, stencil requirements — does the chosen FPGA and connector set impose?

## Board outline and mechanics

- What outline and dimensions are chosen, and what specifically drove them — connector spacing, escape area, or an external constraint?
- Where do the four header sites, the USB connector and any SPI connector sit relative to the board edges, and what keepout does each need for a mating module or cable?
- Are there mounting holes, and what keepout and net (isolated or grounded) do they carry?
- What stack height do attached PMOD modules imply, and does anything on the board interfere with them?
- Does the compactness claim survive a real placement, or does the area have to grow once the escape and fanout are routed?

## Signal integrity, protection and EMC

- Which nets on this board are actually fast enough to matter — USB, the oscillator, SPI at its chosen rate, or any header signal — and what is the evidence for each?
- What return path does each of those nets have across the chosen stackup, and where are the stitching vias?
- Do the externally exposed header, USB and SPI pins get ESD or overvoltage protection, and if not, what is the stated justification?
- What series or termination elements are placed on header signals to control edge rates into unknown attached modules?
- What happens electrically if a user attaches a module that drives a pin the FPGA is also driving?

## Bring-up, test and toolkit integration

- What is the power-on bring-up order in the lab, and what is measured at each step to confirm the documented sequencing assumptions?
- What test points or debug access exist for the rails, the oscillator output and the configuration signals?
- How is each of the four header sites exercised and shown to be fully connected, and how is that test automated?
- How is the USB-to-SPI bridge path verified end to end?
- Which parts of this verification are driven by the shared PCBA_AutoDesignAndTest toolkit, and what board-specific configuration stays in this repository rather than in the toolkit?

## Answers still owed

All of them. See [status.md](status.md).
