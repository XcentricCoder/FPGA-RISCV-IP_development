# FPGA-RISCV-IP_development
This repository is mainly used for completion of tasks assigned for the initial environment setup and RISCV Reference Bring up.

## Where is the RISC-V program located in the vsd-riscv2 repository?
The RISCV program was stored in the load.S file of the repository.

## How is the program compiled and loaded into memory?
The source code of sum1ton.c is is complied for a 64-bit RISC-V processor and produced as an Executable and Linkable object File (elf) named sum1ton.o 
The spike simulator loads it into the simulated RISC-V memory and proxy kernel handles the system calls and provides the runtime environment.

## How does the RISC-V core access memory and memory-mapped IO?
RISC-V is a load-store architecture , menaing that the memory and memory-mapped IO can only be accessed by the load-store instructions happening between the registers and the memory as well as the arithmetic and the logical instructions 

## Where would a new FPGA IP block logically integrate in this system?
A new FPGA block would be logically integrated as a RTL block code conneccted through the SoC interconnect with RISC-V.
/workspaces/vsdfpga_labs/basicRISCV/RTL
