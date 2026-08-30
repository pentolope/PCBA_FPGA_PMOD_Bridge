# Benchmark entry — board 16 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_FPGA_PMOD_Bridge` |
| Board id | `fpga_pmod_bridge` |
| Category | fpga |
| Difficulty | 3 / 5 |
| Brief detail | 2 / 5 |
| Likely layer count | 4 |
| Primary stressors | FPGA escape, multiple voltage rails, clock distribution, connector fanout |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

Category `fpga`, difficulty 3/5, brief detail 2/5 — a mid-difficulty board with a deliberately sparse brief, so most of the architecture is the design agent's to justify rather than to look up. The listed stressors (FPGA escape, multiple voltage rails, clock distribution, connector fanout) are exactly the places where a compact board carrying a self-chosen FPGA package and four external connector sites stops being routable by assertion: the test is whether the agent can pick a device and package, get its pins out and its rails up in the right order, and fan 32 header signals to four mateable sites, citing real device and fabricator data at each step — including for the layer count, which metadata offers only as likely. Because the brief names no part, no voltage and no dimension, it also tests whether the agent can leave those open honestly instead of back-filling invented user requirements.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
