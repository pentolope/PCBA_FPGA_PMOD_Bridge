# Small FPGA Multi-I/O Bridge

A small FPGA board that bridges four PMOD-style connectors to USB and SPI, with four 8-signal headers, configuration flash, an oscillator and all required power rails.

This repository holds the design problem for **PCBA_FPGA_PMOD_Bridge**, a small FPGA board that bridges four PMOD-style connectors to USB and SPI. The brief fixes the functional skeleton — an FPGA with enough I/O for four 8-signal headers, configuration flash, an oscillator, USB connectivity, and all required power rails — and it fixes both endpoints of the bridge: USB and SPI are named, so each has to exist. It also fixes one mechanical intent: the board should be intentionally compact enough that FPGA escape and connector fanout matter. Everything else is left to the design agent: the brief explicitly delegates the FPGA family and package, and it is silent on rail count and voltages, input power source, regulator topology, USB speed class and connector, SPI role and pinout, header pinouts, board dimensions, and stackup — the four layers are metadata's *likely* count, not a stated requirement, so the count itself is still the agent's to justify. The one process obligation attached to that freedom is that the power-sequencing assumptions must be documented. This scaffold records what the brief pins down and what it deliberately leaves open; no part has been selected and no schematic or layout exists yet.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 12 requirements and deliberately leaves
19 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Core function | An FPGA board that bridges four PMOD-style connectors to USB and SPI | brief |
| PMOD-style headers | Four headers, 8 signals each; the chosen FPGA must have enough I/O to serve all four | brief |
| Configuration storage | Configuration flash on the board; type, interface and size unstated | brief |
| Clock source | An oscillator on the board; frequency, output standard and count unstated | brief |
| USB | USB connectivity required; speed class, connector and implementation method unstated | brief |
| SPI | An SPI interface is required as the bridge's second endpoint; role, signal count, rate and physical interface unstated | brief |
| Power rails | All rails the chosen design requires; number, voltages and input source unstated | brief |
| Power sequencing | The sequencing assumptions must be documented | brief |
| FPGA family and package | Explicitly delegated to the designer; no device, family or package named | brief |
| Board size and outline | No dimensions given; the board should be intentionally compact enough that FPGA escape and connector fanout matter | brief |
| Likely layer count | 4 | metadata |
| Category / difficulty / brief detail | fpga / 3 of 5 / 2 of 5 | metadata |
| Primary stressors | FPGA escape, multiple voltage rails, clock distribution, connector fanout | metadata |
| SPI role, signal count, clock rate and physical interface | Not fixed by the brief — design agent's choice | open |
| Header protection, I/O bank voltages and level translation | Not fixed by the brief — design agent's choice | open |
| Final layer count, stackup and plane strategy | Not fixed by the brief — design agent's choice, informed by metadata's likely count of four | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 16 of 32 |
| Category | fpga |
| Difficulty | 3 / 5 |
| Brief detail | 2 / 5 |
| Likely layer count | 4 |
| Primary stressors | FPGA escape, multiple voltage rails, clock distribution, connector fanout |

Category `fpga`, difficulty 3/5, brief detail 2/5 — a mid-difficulty board with a deliberately sparse brief, so most of the architecture is the design agent's to justify rather than to look up. The listed stressors (FPGA escape, multiple voltage rails, clock distribution, connector fanout) are exactly the places where a compact board carrying a self-chosen FPGA package and four external connector sites stops being routable by assertion: the test is whether the agent can pick a device and package, get its pins out and its rails up in the right order, and fan 32 header signals to four mateable sites, citing real device and fabricator data at each step — including for the layer count, which metadata offers only as likely. Because the brief names no part, no voltage and no dimension, it also tests whether the agent can leave those open honestly instead of back-filling invented user requirements.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `.claude/skills/` | the claim-audit and accountability-review skills [CLAUDE.md](CLAUDE.md) requires before a push |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_FPGA_PMOD_Bridge.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `d83d5909ac51f392234e833853a1ffec0276ae79a6ab19266e9302e75ae3a2ed`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
