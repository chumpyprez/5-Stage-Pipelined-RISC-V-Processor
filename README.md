# 5-Stage Pipelined RISC-V Processor

A 5-stage pipelined RISC-V processor designed and implemented at the RTL level using **SystemVerilog**, with supporting C-based program/instruction development and simulation files.

The processor is organized around the conventional five pipeline stages:

**Instruction Fetch (IF) → Instruction Decode (ID) → Execute (EX) → Memory Access (MEM) → Write Back (WB)**

The project contains modular RTL blocks for processor datapath and control, including the ALU, register file, instruction/data memory, instruction decoding, multiplexers, sign/extension logic, and processor-level integration.

> **Note:** Specific ISA instructions, hazard/forwarding mechanisms, and FPGA execution should be documented only where they are supported by the corresponding RTL/testbench files.

## Architecture

![5-Stage RISC-V Pipeline](docs/riscv-5-stage-pipeline.png)

See [ARCHITECTURE.md](ARCHITECTURE.md) for the detailed datapath and pipeline explanation.

## Pipeline Stages

### 1. Instruction Fetch (IF)
Fetches the next instruction using the Program Counter and instruction memory.

### 2. Instruction Decode (ID)
Decodes the instruction, reads source registers, generates immediate values, and prepares control information.

### 3. Execute (EX)
Performs ALU operations, operand selection, address calculation, and comparison/branch-related operations where implemented.

### 4. Memory Access (MEM)
Handles data-memory reads and writes for memory instructions.

### 5. Write Back (WB)
Selects the final result and writes it back to the register file.

## RTL Modules

The project includes modular SystemVerilog blocks such as:

- `alu.sv` — Arithmetic and Logic Unit
- `alu_decoder.sv` — ALU operation decoding
- `controller.sv` — Processor control
- `main_decoder.sv` — Instruction/control decoding
- `datapath.sv` — Processor datapath
- `reg_file.sv` — Register file
- `instr_mem.sv` — Instruction memory
- `data_mem.sv` — Data memory
- `mux2.sv`, `mux3.sv`, `mux4.sv` — Datapath multiplexers
- `sign_extend.sv` — Immediate/sign extension
- `load_extend.sv` — Load-data extension
- `reset_ff.sv` — Resettable sequential logic
- `riscv_cpu.sv` / `riscv_cpu_full.sv` — Processor integration

## Tools & Technologies

- SystemVerilog / Verilog
- C
- RTL design
- Digital logic and computer architecture
- RISC-V ISA concepts
- Simulation and verification
- FPGA/HDL development environment

## Project Goals

- Understand CPU datapath design
- Implement instruction decoding and control
- Build a pipelined processor at RTL
- Develop modular hardware blocks
- Explore RISC-V processor organization
- Verify processor behavior through simulation

## Repository Structure

```text
RISCV-5-Stage-Pipeline/
├── README.md
├── ARCHITECTURE.md
├── docs/
│   └── riscv-5-stage-pipeline.png
├── src/
│   └── RTL source files
└── simulation/
    └── testbench / simulation files
```

## Author

**BM Gagan**  
Electronics and Communication Engineering — PES University
