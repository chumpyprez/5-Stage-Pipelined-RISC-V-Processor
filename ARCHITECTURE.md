# RISC-V 5-Stage Pipeline Architecture

## Overview

The processor is organized into five major pipeline stages:

```text
IF → ID → EX → MEM → WB
```

- **IF** — Instruction Fetch
- **ID** — Instruction Decode
- **EX** — Execute
- **MEM** — Memory Access
- **WB** — Write Back

![RISC-V 5-Stage Pipeline](docs/riscv-5-stage-pipeline.png)

## 1. Instruction Fetch — IF

The IF stage obtains the next instruction from instruction memory using the Program Counter (PC).

**Responsibilities**
- Maintain/update the PC
- Fetch instructions
- Generate the next instruction address

## 2. Instruction Decode — ID

The ID stage interprets the fetched instruction and prepares operands and control information.

**Responsibilities**
- Decode instruction fields
- Read source registers
- Identify destination register
- Generate immediate values
- Generate control information

Relevant modules include:

```text
reg_file.sv
main_decoder.sv
sign_extend.sv
controller.sv
```

## 3. Execute — EX

The EX stage performs the operation selected by the decoded instruction.

**Responsibilities**
- Arithmetic and logical operations
- Operand selection
- Address calculation
- Comparison/branch-related operations where implemented

Relevant modules include:

```text
alu.sv
alu_decoder.sv
mux2.sv
mux3.sv
mux4.sv
```

## 4. Memory Access — MEM

The MEM stage handles data-memory operations.

**Responsibilities**
- Read data for load operations
- Write data for store operations
- Pass the ALU result toward write back

Main module:

```text
data_mem.sv
```

## 5. Write Back — WB

The WB stage selects the final result and writes it to the register file.

Typical sources are:

```text
ALU Result ──┐
             ├──> Write-Back MUX ──> Register File
Memory Data ─┘
```

## Pipeline Data Flow

```text
Instruction
    |
    v
+-----------+
|    IF     |  Fetch
+-----+-----+
      |
      v
+-----------+
|    ID     |  Decode + Register Read
+-----+-----+
      |
      v
+-----------+
|    EX     |  ALU / Address / Compare
+-----+-----+
      |
      v
+-----------+
|   MEM     |  Data Memory
+-----+-----+
      |
      v
+-----------+
|    WB     |  Register Write
+-----------+
```

## Major RTL Blocks

| Module | Purpose |
|---|---|
| `alu.sv` | Arithmetic and logical operations |
| `alu_decoder.sv` | ALU operation selection |
| `controller.sv` | Processor control |
| `main_decoder.sv` | Instruction/control decoding |
| `datapath.sv` | Main processor datapath |
| `reg_file.sv` | Register file |
| `instr_mem.sv` | Instruction memory |
| `data_mem.sv` | Data memory |
| `mux2.sv` | Two-input selection |
| `mux3.sv` | Three-input selection |
| `mux4.sv` | Four-input selection |
| `sign_extend.sv` | Immediate extension |
| `load_extend.sv` | Load-data extension |
| `reset_ff.sv` | Resettable sequential logic |
| `riscv_cpu.sv` | Processor integration |
| `riscv_cpu_full.sv` | Full processor integration |

## Pipeline Timing

A pipelined processor overlaps instructions across stages:

```text
Cycle       1    2    3    4    5    6    7
------------------------------------------------
Instr. 1   IF   ID   EX   MEM  WB
Instr. 2        IF   ID   EX   MEM  WB
Instr. 3             IF   ID   EX   MEM  WB
Instr. 4                  IF   ID   EX   MEM  WB
```

This allows multiple instructions to be in different stages simultaneously.

## Verification

Simulation should be used to verify:

- Program-counter progression
- Register-file updates
- ALU outputs
- Memory accesses
- Control signals
- Final architectural results

Place verified testbench files under `simulation/`.

> Hazard detection, forwarding, stalling, branch prediction, and exact ISA coverage should only be listed as implemented features when supported by the final RTL.

