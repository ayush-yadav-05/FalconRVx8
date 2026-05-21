# FalconRVx8
# FalconRVx8: Custom RISC-V Processor on FPGA

**FalconRVx8** is a custom RISC-V processor implemented on an FPGA. It uses a pipelined processor architecture supporting the RV32I instruction set along with the RV32M multiply/divide extension. The project also includes a small FPGA-based SoC environment with instruction memory, data memory, a bus interconnect, UART communication, and LED-based hardware debugging.

The processor runs a bare-metal C program from FPGA memory and communicates with a PC through a UART serial interface. Using a PuTTY terminal, the system behaves like an interactive calculator: the user enters expressions such as `12*3`, the processor executes the program internally, and the result is printed back through UART.

---

## Overview

FalconRVx8 is designed as a learning-focused FPGA processor project that connects CPU architecture with real hardware execution. Instead of only simulating instructions, the processor is integrated into a complete FPGA system capable of running compiled C programs.

The design includes:

- A custom RISC-V CPU core
- Instruction and data memories initialized using hex files
- A memory-mapped UART peripheral
- A simple bus interconnect
- LED debug outputs for observing processor activity
- A C-to-hex build flow for changing the program running on the CPU

The current demo program is a UART-based calculator. After programming the FPGA, the user can open a serial terminal, reset the board, and interact with the processor directly.

---

## Key Features

- **Custom RISC-V Processor**
  - Implements a practical RV32I-based processor core
  - Supports arithmetic, logical, load/store, branch, jump, and upper-immediate instructions

- **RV32M Extension Support**
  - Supports multiply and divide instructions including:
    - `MUL`
    - `MULH`
    - `MULHSU`
    - `MULHU`
    - `DIV`
    - `DIVU`
    - `REM`
    - `REMU`

- **Pipelined Architecture**
  - Uses a multi-stage processor structure
  - Includes stall, flush, and bypass logic for correct instruction execution

- **UART-Based Interactive Execution**
  - Communicates with a PC using UART at `115200 baud`
  - Works with PuTTY or any serial terminal
  - Runs an interactive calculator program on the custom CPU

- **Memory-Mapped I/O**
  - UART peripheral is accessed through fixed memory addresses
  - Software can send and receive characters using normal load/store operations

- **C Program Execution**
  - Bare-metal C programs are compiled using a RISC-V GCC toolchain
  - Generated hex files initialize FPGA instruction and data memories

- **LED Debugging**
  - FPGA LEDs show useful internal activity such as:
    - clock heartbeat
    - reset state
    - UART activity
    - instruction fetch
    - memory access
    - stall/error indicators

- **FPGA Target**
  - Designed for the Digilent Nexys A7-100T board
  - Uses Xilinx Vivado for synthesis, implementation, and bitstream generation

---

## Project Structure

```text
FalconRVx8/
├── modules/
│   ├── fpga_top.v
│   ├── constraints.xdc
│   ├── soc/
│   │   └── soc_top.v
│   ├── cpu core/
│   │   ├── pipeline.v
│   │   ├── IF_ID.v
│   │   ├── execute.v
│   │   ├── wb.v
│   │   ├── mul_module.v
│   │   ├── div_module.v
│   │   └── opcode.vh
│   ├── memory/
│   │   ├── memory.v
│   │   ├── imem.hex
│   │   └── dmem.hex
│   ├── bus/
│   │   └── bus.v
│   └── uart/
│       ├── uart_peripheral.v
│       ├── uart_tx.v
│       └── uart_rx.v
│
├── mem generator/
│   ├── c code/
│   ├── build files/
│   └── hex files/
│
├── fpga_top.bit
├── Makefile
└── README.md
