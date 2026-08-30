# Sources — Small FPGA Multi-I/O Bridge

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| FPGA device datasheet and package files (pin/ball map, pitch, dimensions) | Fixes the usable I/O count per bank, clock-capable pins, package pitch and the geometry every escape claim depends on. |
| FPGA power-supply and sequencing documentation (datasheet DC/power section, vendor sequencing app notes) | The brief requires the power-sequencing assumptions to be documented; the required order, ramp and monitoring must come from the device's own specification. |
| FPGA configuration user guide | Sets which configuration mode is legal, what flash interface and voltage it needs, and the pin states required during power-up. |
| Configuration flash datasheet | Supply voltage, interface width, timing and capacity must match the configuration mode selected. |
| Oscillator or clock source datasheet | Frequency, output standard, jitter, supply current and enable behaviour feed both the clock distribution plan and the rail budget. |
| Datasheets for the regulators and power-management devices actually chosen, whatever topology they use | Enable/soft-start behaviour, dropout or efficiency, and thermal derating substantiate the rail and sequencing design in a compact area. |
| USB specification and/or USB interface device datasheet | Supplies the differential impedance target, length and matching limits, and bus-power current rules for whatever speed class is chosen. |
| PMOD interface specification | Any claim of PMOD-style compatibility for the four 8-signal sites has to be measured against the published pinout and electrical conventions rather than assumed. |
| Fabricator capability and stackup documentation for the layer count the design settles on | Minimum trace/space, drill, annular ring and via technology decide whether the FPGA escape is manufacturable at all, and the stackup table sets the impedance geometry. |
| Assembly house process capability and part availability data | Package placement limits, double-sided assembly and real stock for the chosen FPGA and connectors constrain the selection. |
| Connector datasheets and mating/mechanical drawings (USB, headers, any SPI interface) | Footprint, keepout, retention and mating-module envelope drive the compact outline and the fanout geometry. |
| ESD/EMC test-level standards and protection device datasheets, if protection is fitted | Any protection claim on externally exposed header, USB or SPI pins needs a stated level and a device whose clamping and capacitance suit the signal rates. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
