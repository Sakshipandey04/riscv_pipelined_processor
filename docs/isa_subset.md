# ISA Subset — RV32I

## Instruction Formats

| Format | Fields |
|--------|--------|
| R-type | funct7 \| rs2 \| rs1 \| funct3 \| rd \| opcode |
| I-type | imm[11:0] \| rs1 \| funct3 \| rd \| opcode |
| S-type | imm[11:5] \| rs2 \| rs1 \| funct3 \| imm[4:0] \| opcode |
| B-type | imm[12,10:5] \| rs2 \| rs1 \| funct3 \| imm[4:1,11] \| opcode |
| J-type | imm[20,10:1,11,19:12] \| rd \| opcode |

## Supported Instructions

(Fill in opcode/funct3/funct7 for each instruction as you implement it)

| Instruction | Format | opcode | funct3 | funct7 |
|-------------|--------|--------|--------|--------|
| add | R | 0110011 | 000 | 0000000 |
| sub | R | 0110011 | 000 | 0100000 |
| ... | | | | |
