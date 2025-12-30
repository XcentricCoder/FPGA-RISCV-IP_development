# Basic RISC-V SoC (RV32I) with GPIO & UART

A minimal **bare-metal RISC-V RV32I System-on-Chip** implemented from scratch in Verilog, with:
- Custom RISC-V CPU core
- BRAM-based instruction/data memory
- Memory-mapped GPIO
- Memory-mapped UART
- Clock & reset generation
- Simulation support (Icarus Verilog + GTKWave)
- FPGA-ready flow (iCE40)

This project is intended for **learning SoC bring-up**, not performance.

---

## Features

- RV32I integer instruction set
- Single-cycle / simple FSM CPU
- Memory-mapped peripherals
- Bare-metal firmware (no OS, no libc)
- Deterministic simulation
- Clean separation of RTL and firmware

---

## Project Structure

basicRISCV/
├── RTL/
│ ├── riscv.v # Top-level SoC (CPU + Memory + IO)
│ ├── clockworks.v # Clock & reset logic
│ ├── gpio_ip.v # GPIO peripheral
│ ├── emitter_uart.v # UART transmitter
│ ├── tb_soc.v # Testbench
│ ├── firmware.hex # Firmware loaded into BRAM (simulation)
│ └── Makefile # FPGA build (iCE40)
│
├── Firmware/
│ ├── gpio_test.c # Bare-metal test program
│ ├── start.S # Reset entry point
│ ├── bram.ld # Linker script
│ ├── Makefile # Firmware build system
│ └── firmware_words # ELF → HEX converter
│
└── README.md



---

## Memory Map

| Address        | Description      |
|---------------|------------------|
| `0x00000000`  | BRAM (code/data) |
| `0x00400008`  | UART TX register |
| `0x00400020`  | GPIO register    |

---

## GPIO

- 32-bit output register
- Lower 5 bits drive LEDs

### Example (firmware)
```c
*(volatile unsigned int *)(0x00400020) = 0xDEADBEEF;
```
## UART

-Transmit-only UART
-Memory-mapped
-Baud rate configurable in RTL
```
*(volatile unsigned int *)(0x00400008) = 'G';
```
### Firmware Model

- Bare-metal
- No startup runtime
- No printf
- No interrupts
- Execution starts at _start → main

### Correct startup (start.S)

## Buillding Firmware
- From the Firmware directory
  ```
  make clean
  make gpio_test.bram.elf
  make gpio_test.hex
  ```
- This generates firmware.hex and copies it into RTL/.

- From the RTL directory

   ```
  iverilog -g2012 -DBENCH -DSIMULATION -DCPU_FREQ=50 \
  tb_soc.v riscv.v clockworks.v gpio_ip.v emitter_uart.v

  vvp a.out
   ```

- For viewing the waveform

  ```
  gtkwave soc_gpio.vcd

  ```

  

  
