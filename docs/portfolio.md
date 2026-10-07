# Portfolio wording

## Project title

**FPGA General-Purpose Processor / 8-bit ALU — VHDL and Quartus II**

## Resume summary

Designed an FSM-controlled 8-bit processing unit in VHDL, integrating operand registers, one-hot operation decoding, arithmetic/logic functions, and seven-segment output; documented expected results and Quartus simulation waveforms across baseline and assigned ALU variants.

## Optional hardware bullet

Implemented the course processor on an Altera FPGA board with seven-segment output and a student-ID-driven odd/even display extension.

The hardware bullet relies on the author's deployment account. Add the exact board model only after confirming it; the archive identifies a Cyclone II device in a component build, not a verified board model or complete processor build.

## Suggested GitHub description

VHDL 8-bit processor/ALU with FSM control, operand registers, one-hot decoding, seven-segment output, and archived Quartus waveform verification.

## Suggested repository name and topics

Suggested name: `fpga-8bit-processor`. The existing remote has not been renamed.

Suggested topics: `vhdl`, `fpga`, `alu`, `finite-state-machine`, `quartus`, `digital-design`, `computer-architecture`, `seven-segment-display`.

Avoid claiming 16 implemented instructions, a stored-program CPU, exhaustive verification, full-system timing closure, or measured performance/resource improvements. Nine baseline functions and nine assigned functions are separate ALU variants, not 18 simultaneously selectable instructions.
