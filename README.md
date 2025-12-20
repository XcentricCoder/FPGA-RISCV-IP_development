# Task-1: Environment Setup & RISC-V Reference Bring-Up

## Overview
This repository documents the successful completion of **Task-1: Environment Setup & RISC-V Reference Bring-Up** as part of the VSDFPGA learning track.

The objective of this task is to:
- Set up a stable development environment using **GitHub Codespaces**
- Verify the **RISC-V reference execution flow**
- Clone and run **VSDFPGA labs** that do not require FPGA hardware

This task focuses on **toolchain readiness and execution flow verification**, not FPGA programming.

---

## Environment
- **Platform:** GitHub Codespaces  
- **Operating System:** Linux (Codespace default)
- **Toolchain:** Preconfigured RISC-V toolchain from `vsd-riscv2`
- **FPGA Hardware:** Not required

---

## Step 1: GitHub Codespace Setup ✅
- Forked the official repository:  
  https://github.com/vsdip/vsd-riscv2
- Launched GitHub Codespaces successfully
- Verified that the Codespace builds and opens without errors

**Result:** Codespace environment initialized successfully.

![Outcome](https://github.com/XcentricCoder/FPGA-RISCV-IP_development/blob/main/Screenshot%202025-12-21%20003539.png)

---

## Step 2: RISC-V Reference Flow Verification ✅
Inside the `vsd-riscv2` Codespace:

- Followed the README instructions
- Built the provided fundamental RISC-V program
- Executed the program successfully
- Observed correct console output with no build or runtime errors

### Outcome
- ✅ RISC-V program runs successfully  
- ✅ Toolchain verified and functional  
- ✅ No build or execution issues  

![Outcome](https://github.com/XcentricCoder/FPGA-RISCV-IP_development/blob/main/Screenshot%202025-12-19%20193946.png)


---

## Step 3: Clone and Run VSDFPGA Labs ✅
After verifying the RISC-V reference flow:

```bash
git clone https://github.com/vsdip/vsdfpga_labs.git
cd vsdfpga_labs
```

- Followed the instructions provided in the repository
  ![Outcome](https://github.com/XcentricCoder/FPGA-RISCV-IP_development/blob/main/Screenshot%202025-12-20%20011417.png)
- Built and ran basic labs that do not require FPGA hardware
 ```bash
riscv64-unknown-elf-gcc -o riscv_logo.o riscv_logo.c
spike pk riscv_logo.o
```
  ![Outcome](https://github.com/XcentricCoder/FPGA-RISCV-IP_development/blob/main/Screenshot%20(122).png)
  ![Outcome](https://github.com/XcentricCoder/FPGA-RISCV-IP_development/blob/main/Screenshot%202025-12-20%20122137.png)
- Verified successful execution through simulation output and logs
  ![Outcome](https://github.com/XcentricCoder/FPGA-RISCV-IP_development/blob/main/Screenshot%202025-12-20%20003521.png)
- FPGA tools (yosys, nextpnr, programmers, drivers) must NOT be installed. Hence, firmware was built but bitstream generation and FPGA flashing wasn't possible at this stage.
  ![Outcome](https://github.com/XcentricCoder/FPGA-RISCV-IP_development/blob/main/Screenshot%202025-12-20%20003620.png)
## Outcome
- ✅ Multi-repository workflow verified
- ✅ VSDFPGA labs executed successfully (simulation-based)
- ✅ Generated BRAM hex from firmware
- ✅ Environment ready for IP and SoC-level development tasks

## Notes
- FPGA hardware and USB serial devices are not required for this task
- Serial terminal tools (e.g., picocom) are not supported in GitHub Codespaces due to lack of USB passthrough
- All mandatory objectives for Task-1 have been completed successfully

## Repositories forked
- https://github.com/vsdip/vsd-riscv2
- https://github.com/vsdip/vsdfpga_labs.git

## Questions

### Where is the RISC-V program located in the vsd-riscv2 repository?
The RISCV program was stored in the load.S file of the repository.

### How is the program compiled and loaded into memory?
The source code of sum1ton.c is is complied for a 64-bit RISC-V processor and produced as an Executable and Linkable object File (elf) named sum1ton.o 
The spike simulator loads it into the simulated RISC-V memory and proxy kernel handles the system calls and provides the runtime environment.

### How does the RISC-V core access memory and memory-mapped IO?
RISC-V is a load-store architecture , menaing that the memory and memory-mapped IO can only be accessed by the load-store instructions happening between the registers and the memory as well as the arithmetic and the logical instructions 

### Where would a new FPGA IP block logically integrate in this system?
A new FPGA block would be logically integrated as a RTL block code conneccted through the SoC interconnect with RISC-V.
/workspaces/vsdfpga_labs/basicRISCV/RTL

## Notes
## Conclusion

Task-1 was completed successfully by setting up the development environment, validating the RISC-V reference execution flow, and running VSDFPGA labs without requiring FPGA hardware. This confirms toolchain readiness, correct workflow understanding, and preparedness for upcoming IP and FPGA development tasks.

