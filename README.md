# 5-Stage Pipelined RISC-V Processor

A 32-bit pipelined RISC-V processor (RV32I subset) implemented in Verilog HDL, 
featuring hazard detection, data forwarding, and branch handling. Verified 
functionally in ModelSim and synthesized using Xilinx Vivado.

## Features

- Classic 5-stage pipeline: IF → ID → EX → MEM → WB
- Data hazard resolution via forwarding (EX/MEM and MEM/WB → EX)
- Load-use hazard detection with automatic pipeline stalling
- Control hazard handling with branch flush (predict-not-taken)
- Modular design: separate ALU, control unit, register file, hazard/forwarding units
- Self-checking testbench with pass/fail reporting

## Instruction Set Supported

| Type | Instructions |
|------|--------------|
| R-type | add, sub, and, or, xor, slt |
| I-type | addi, andi, ori, slti, lw |
| S-type | sw |
| B-type | beq, bne |
| J-type | jal |

Full instruction encoding details: [docs/isa_subset.md](docs/isa_subset.md)

## Architecture

![Pipeline Block Diagram](docs/block_diagram.png)

Hazards are handled as follows:
- **RAW data hazards**: resolved by forwarding results from EX/MEM and 
  MEM/WB pipeline registers directly into the EX stage inputs.
- **Load-use hazard**: detected by the hazard detection unit; pipeline 
  stalls for one cycle since the loaded value isn't available until MEM.
- **Control hazards**: branches assumed not-taken; IF/ID and ID/EX flushed 
  if the branch resolves as taken.

## Repository Structure

- `rtl/` — Verilog source for all pipeline modules
- `testbench/` — Testbench and hand-assembled test programs (`.mem` files)
- `sim/modelsim/` — ModelSim simulation scripts
- `synth/vivado/` — Vivado constraints and synthesis reports
- `docs/` — Block diagrams, ISA reference, control signal tables, final report

## How to Simulate (ModelSim)

\`\`\`bash
cd sim/modelsim
vsim -do run_sim.do
\`\`\`

Or manually:
\`\`\`bash
vlog ../../rtl/*.v ../../rtl/pipeline_regs/*.v ../../testbench/riscv_top_tb.v
vsim riscv_top_tb
run -all
\`\`\`

## How to Synthesize (Vivado)

1. Open Vivado → create new project → add all files from `rtl/`
2. Add `synth/vivado/constraints.xdc` as the constraints file
3. Run Synthesis → Run Implementation → Generate Bitstream
4. Utilization and timing reports will appear under Vivado's Reports tab

## Test Programs

| Program | Purpose |
|---------|---------|
| `basic_alu.mem` | Verifies core arithmetic/logic instructions |
| `raw_hazard.mem` | Back-to-back dependent instructions — tests forwarding |
| `load_use_hazard.mem` | `lw` immediately followed by dependent use — tests stalling |
| `branch_test.mem` | Taken/not-taken branches — tests flush logic |

## Results

| Metric | Value |
|--------|-------|
| LUT utilization | TBD |
| Max frequency | TBD |
| Target device | TBD |

(Fill in after running synthesis)

## Author

Sakshi Pandey- Dronacharya Group of Institutions, Greater Noida, ECE,

## License

MIT License — see [LICENSE](LICENSE)
