# SAP-1 Computer with Control Sequencer

An 8-bit SAP (Simple-As-Possible) computer implementation featuring a complete 
instruction set, control sequencer, and timing logic — built and verified as part 
of the VLSI Technology Sessional (ETE 404), Dept. of ETE, CUET.

## Overview
This project implements the SAP-1 architecture at the microarchitecture level, 
demonstrating fetch-decode-execute cycles, instruction timing (T-states), and 
control signal sequencing for a minimal CPU.

## Problem Demonstrated
Compute **(5 + 2) − 4** using the following SAP-1 assembly program:
1: LDA 10 ; Load value from memory address 10 (0x0A)
2: ADD 9 ; Add value from memory address 9 (0x09)
3: SUB 8 ; Subtract value from memory address 8 (0x08)
4: OUT ; Output result

## Instruction Set Supported
| Opcode | Mnemonic | Function |
|--------|----------|----------|
| 0001 | LDA | Load accumulator from memory |
| 0010 | ADD | Add memory value to accumulator |
| 0011 | SUB | Subtract memory value from accumulator |
| 1110 | OUT | Output accumulator value |

## Programming & Execution Steps
The system is programmed in **user mode (u_mode)** with **debug mode** enabled, 
manually writing instructions and data into SRAM via `mar_in_en` and `sram_wr` 
control signals before switching to **output mode (o_mode)** to run the 
fetch-decode-execute cycle.

1. Load instructions and operand data into SRAM at specified addresses
2. Reset the program counter (`pc_reset`)
3. Step through clock pulses to observe T-state transitions
4. Verify result in the accumulator/register after each instruction executes

## Timing Diagram (T-States)

| T-State | LDA (0001) | ADD (0010) | SUB (0011) | OUT (1110) |
|---------|-----------|-----------|-----------|-----------|
| T1 | PC_out, MAR_in_en | PC_out, MAR_in_en | PC_out, MAR_in_en | PC_out, MAR_in_en |
| T2 | SRAM_rd, IR_in_en | SRAM_rd, IR_in_en | SRAM_rd, IR_in_en | SRAM_rd, IR_in_en |
| T3 | PC_en | PC_en | PC_en | PC_en |
| T4 | IR_out_en, MAR_in_en | IR_out_en, MAR_in_en | IR_out_en, MAR_in_en | ALU_out |
| T5 | SRAM_rd, A_in | SRAM_rd, B_in | SRAM_rd, B_in | — |
| T6 | — | ALU_out, A_in | ALU_out, A_in, ALU_sub | — |

## Tools Used
- Digital logic simulation environment (SAP-1 CPU model)
- Manual control-signal programming via debug interface

## Author
Md. Emran Hossain Dipu (ID: 1908028) — Dept. of ETE, CUET  
Course: VLSI Technology Sessional (ETE 404)  
Instructor: Arif Istiaque Rupom, Lecturer, Dept. of ETE
