# Task 2 — Proving RISC-V Toolchain Setup (Run, Disassemble, Decode)

This repository is part of the VSD RISC-V SoC Workshop.

In Task 2, the goal is to prove that the RISC-V toolchain is correctly installed and functional on the local machine.

---

## Steps Performed

- Compiled 4 unique C programs using `riscv64-unknown-elf-gcc`
- Embedded `USERNAME`, `HOSTNAME`, `MACHINE_ID`, and timestamps for build uniqueness
- Ran each program on the RISC-V simulator: `spike pk`
- Captured disassembly (`.objdump`) and source-level assembly (`.s`) of each
- Manually decoded at least 5 RISC-V integer instructions
- Documented all outputs, binaries, and screenshots as evidence

---

## Toolchain Verification

### Spike Version

Output of:
```bash
spike -version
```

Note: `spike --help | head -1` was used instead of `spike -version`.

### RISC-V GCC Version

Output of:
```bash
riscv64-unknown-elf-gcc -v
```

---

## Compile Commands

<details>
<summary>For <code>factorial.c</code></summary>

```bash
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
factorial.c -o factorial
```

</details>

<details>
<summary>For <code>max_array.c</code></summary>

```bash
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
max_array.c -o max_array
```

</details>

<details>
<summary>For <code>bitops.c</code></summary>

```bash
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bitops.c -o bitops
```

</details>

<details>
<summary>For <code>bubble_sort.c</code></summary>

```bash
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bubble_sort.c -o bubble_sort
```

</details>

---

## Proof of Uniqueness

Each program output includes a clearly visible ProofID and RunID, generated using a 64-bit FNV-1a hash based on the following fields:

- USERNAME
- HOSTNAME
- MACHINE_ID
- BUILD_UTC
- BUILD_EPOCH
- Program name

These fields ensure that the build is uniquely tied to my machine and identity.

---

## Evidence

All screenshots and output files (e.g., `factorial_output.png`, `bitops_output.png`) clearly show these values for verification and traceability.

