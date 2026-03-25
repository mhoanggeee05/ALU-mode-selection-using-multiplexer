#  ALU mode selection using multiplexer (Structural Design)

## Overview
8-bit ALU implemented in SystemVerilog using structural design. 
Supports arithmetic, logic, and shift operations with registered inputs and outputs.

## Features
- ADD/SUB (2’s complement)
- Shift left / right using MUX (no shift operator)
- AND, OR, XOR, NOT
- 3-bit control signal (`sel`)
- Overflow and carry detection
- Registered datapath (synchronous design)

## Structure
- `ALU`: main operation selection (MUX-based)
- `EBA + FA`: ripple-carry adder/subtractor
- `shiftreg`: structural shifters (left/right)
- `logic blocks`: AND, OR, XOR, NOT
- `nbitreg / d_ff`: registers and flags

## Notes
- Fully structural implementation (minimal behavioral code)
- Shift amount limited by B[2:0]
- Verified through simulation
