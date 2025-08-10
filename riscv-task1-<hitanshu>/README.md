# Task 2 — Proving RISC-V Toolchain Setup (Run, Disassemble, Decode)

## This repository is part of the VSD RISC-V SoC Workshop. In Task 2, the goal is to prove that the RISC-V toolchain is correctly installed and functional on the local machine.

## The following steps were performed: -
- Compiled 4 unique C programs using `riscv64-unknown-elf-gcc`
- Embedded user, host, machine ID, and timestamps for build uniqueness
- Ran each program on the RISC-V simulator (`spike pk`)
- Captured disassembly (`.objdump`) and source-level assembly (`.s`) of each
- Manually decoded at least 5 RISC-V integer instructions
- Documented all outputs, binaries, and screenshots as evidence

## Toolchain Verification

### riscv64-unknown-elf-gcc -v
## Output of ``` riscv64-unknown-elf-gcc -v ```
![WhatsApp Image 2025-08-10 at 12 16 55_7917fb11](https://github.com/user-attachments/assets/2406b237-ace9-4941-9184-6ed06ce27b67)

### Spike Version
## Output of ``` spike -version ```
# (Note: - ``` spike --help ``` used instead of ``` spike -version```)
![WhatsApp Image 2025-08-10 at 12 16 56_9592b73a](https://github.com/user-attachments/assets/640d6eb4-85bd-4c09-9b3c-01ffe99d02d2)


### Compile Commands: -

#### For factorial.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
factorial.c -o factorial
```
#### For max_array.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
max_array.c -o max_array
```
#### For bitops.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bitops.c -o bitops
```
## For bubble_sort.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bubble_sort.c -o bubble_sort
```

## Proof of Uniqueness

## Each program output includes a clearly visible `ProofID` and `RunID`, which are generated using a 64-bit FNV-1a hash based on: -

- `USERNAME`
- `HOSTNAME`
- `MACHINE_ID`
- `BUILD_UTC`
- `BUILD_EPOCH`
- `Program name`

## These fields ensure the build is unique to my machine and identity. All screenshots and output files (e.g., `factorial_output.png`, `bitops_output.png`) clearly show these values for verification.



