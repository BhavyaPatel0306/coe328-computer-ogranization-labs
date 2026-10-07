# Reproduction and repository organization

## Current archive

The repository includes VHDL backups (`.vhd.bak`), schematic designs (`.bdf`), symbols (`.bsf`), waveform files (`.vwf`), and an original report. It does not include Quartus project (`.qpf`) or assignment (`.qsf`) files. Original directories are preserved because moving files before resolving entity references would make recovery harder.

The archived flow report identifies Quartus II 13.0.1 SP1 and device EP2C35F672C6. Select a Quartus installation with support for the actual target device; this documentation does not establish compatibility with newer releases or any particular development board.

## Recovery procedure

1. Make a separate working copy. Recover final VHDL originals if available; otherwise copy `.vhd.bak` files to `.vhd` in the recovery workspace while retaining the archive.
2. Create a Quartus project for each problem and choose the corresponding `.bdf` as the intended top-level design. Add required VHDL components and search paths.
3. Reconcile entity names before generating symbols. The saved register declares `latch1`, the decoder declares `Decoder4to16`, and the FSM declares `FSM`, whereas schematics use names such as `latchcode`, `decodercode`, and `FSMcode`. Problem 1 uses further `*prob1` names. Problem 2 declares `ALUcode`, but its schematic references `ALUproblem2code`.
4. Resolve the Problem 2 `LR2` typo in the recovery copy. Treat the rotate-right versus required rotate-left discrepancy as a separate functional change, with explicit verification. Do not silently rewrite the archived submission.
5. Recover `ALUproblem3code` or deliberately reconstruct a new documented FSM/display-only top level. Resolve this reference before calling the existing schematic complete.
6. Regenerate symbols and inspect every port and bus connection. Confirm reset polarities, decoder/FSM enables, output nibble order, and display segment conventions.
7. Restore verified board assignments from the actual board manual and original project if available. Do not reuse the archived `ssegcode` component pin file as the full processor pinout.
8. Compile and run functional simulations using the provided `.vwf` files after reconciling node names. Follow the [verification checklist](verification.md), then document synthesis and board programming separately.

The source mixes `std_logic_unsigned` with `numeric_std`. A future portability cleanup should standardize arithmetic packages in a separate, tested change.

## Recommended future layout

The documentation layer is implemented now. Once a working build has been recovered, a subsequent migration could separate:

```text
rtl/common/                Canonical register, FSM, decoder, display VHDL
rtl/problem1/              Baseline ALU
rtl/problem2/              Assigned ALU
quartus/problem1/          Project settings and top-level schematic
quartus/problem2/          Project settings and top-level schematic
quartus/problem3/          Recovered extension project
sim/                      Waveforms and repeatable verification inputs
docs/assets/               Screenshots with provenance and captions
archive/                   Original submission and historical build artifacts
```

Perform the move alongside regenerated symbols, updated paths, and a successful rebuild. Preserve the report and source history. Generated caches can be ignored, but do not broadly ignore `*.bak` while these files are the only VHDL sources, or remove existing programming artifacts before their provenance is recorded.
