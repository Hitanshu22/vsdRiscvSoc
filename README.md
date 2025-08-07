# vsdRiscvSoc

# Task 1 – RISC-V Toolchain Setup & Uniqueness Test (VSD SoC Lab)

This repository documents the steps and verification outputs for **Task 1** of the **VSD RISC-V SoC Lab**. The task includes setting up the complete RISC-V GCC toolchain, building the Spike ISA simulator and Proxy Kernel, and validating the setup by compiling and running a uniqueness test program.

---

## What's Implemented

- Installed the RISC-V toolchain (`riscv64-unknown-elf-gcc`)
- Built and tested **Spike** (ISA simulator)
- Installed and verified **Proxy Kernel (pk)**
- Ran a C-based **uniqueness test** on `spike pk`
- Platform: Rocky Linux (RHEL-based alternative to Ubuntu)

---

## Table of Contents

1. [Install base developer tools](#task-1--install-base-developer-tools)  
2. [Create a clean workspace](#task-2--create-clean-workspace)  
3. [Get a prebuilt RISC‑V GCC toolchain](#task-3--download-prebuilt-riscv-gcc-toolchain)  
4. [Add toolchain to your PATH](#task-4--add-toolchain-to-path)  
5. [Install Device Tree Compiler (DTC)](#task-5--install-device-tree-compiler-dtc)  
6. [Build and install Spike](#task-6--build-and-install-spike-isa-simulator)  
7. [Build and install Proxy Kernel (riscv-pk)](#task-7--build-and-install-proxy-kernel)  
8. [Add cross-bin directory to PATH](#task-8--add-cross-bin-directory-to-path)  
9. [Install Icarus Verilog (optional)](#task-9--optional-install-icarus-verilog)  
10. [Perform sanity checks](#task-10--sanity-checks)  
11. [Final uniqueness test and output](#final-deliverable-unique-c-test)  
12. [Conclusion](#conclusion)


## Results

- **Source file**: [`unique_test.c`](./unique_test.c)  
- **Program Output from** `spike pk ./unique_test`: [`Output`](./Output.txt)


## Environment Setup & Execution Steps

### Task 1 — Install Base Developer Tools

```bash
sudo apt-get install -y git vim autoconf automake autotools-dev curl \
libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex \
texinfo gperf libtool patchutils bc zlib1g-dev libexpat1-dev gtkwave
```

### Task 2 — Create Clean Workspace

```bash
cd
pwd=$PWD
mkdir -p riscv_toolchain
cd riscv_toolchain
```

### Task 3 — Download Prebuilt RISC‑V GCC Toolchain

```bash
wget "https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz"
tar -xvzf riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz
```
![alt text](<WhatsApp Image 2025-08-07 at 21.56.58_688a8546.jpg>)
### Task 4 — Add Toolchain to PATH

**Temporary (current shell):**

```bash
export PATH=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH
```

**Persistent (all terminals):**

```bash
echo 'export PATH=$HOME/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH' >> ~/.bashrc
```
[text](<WhatsApp Image 2025-08-07 at 21.56.57_fac61c9f.jpg>)
### If you get error:

> `riscv64-unknown-elf-gdb: error while loading shared libraries: libncurses.so.5`

**Run:**

```bash
cd /tmp
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libtinfo5_6.3-2ubuntu0.1_amd64.deb
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libncurses5_6.3-2ubuntu0.1_amd64.deb
sudo dpkg -i libtinfo5_6.3-2ubuntu0.1_amd64.deb
sudo dpkg -i libncurses5_6.3-2ubuntu0.1_amd64.deb
```
![alt text](<WhatsApp Image 2025-08-07 at 22.15.24_d6220834.jpg>)
### Task 5 — Install Device Tree Compiler (DTC)

```bash
sudo apt-get install -y device-tree-compiler
```

### Task 6 — Build and Install Spike (ISA Simulator)

```bash
git clone https://github.com/riscv/riscv-isa-sim.git
cd riscv-isa-sim
mkdir -p build && cd build
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14
make -j$(nproc)
sudo make install
```

### Task 7 — Build and Install Proxy Kernel

```bash
cd $pwd/riscv_toolchain
git clone https://github.com/riscv/riscv-pk.git
cd riscv-pk
mkdir -p build && cd build
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14 --host=riscv64-unknown-elf
make -j$(nproc)
sudo make install
```

### Task 8 — Add Cross Bin Directory to PATH

**Current shell:**

```bash
export PATH=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH
```

**Persistent:**

```bash
echo 'export PATH=$HOME/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

### Task 9 — (Optional) Install Icarus Verilog

```bash
cd $pwd/riscv_toolchain
git clone https://github.com/steveicarus/iverilog.git
cd iverilog
git checkout --track -b v10-branch origin/v10-branch
git pull
chmod +x autoconf.sh
./autoconf.sh
./configure
make -j$(nproc)
sudo make install
```

### Task 10 — Sanity Checks

```bash
which riscv64-unknown-elf-gcc
riscv64-unknown-elf-gcc -v
which spike
spike --version
which pk
```
![alt text](<WhatsApp Image 2025-08-07 at 19.47.55_6b6ba80d.jpg>)
![alt text](<WhatsApp Image 2025-08-07 at 19.47.54_e634b506.jpg>)
![alt text](<WhatsApp Image 2025-08-07 at 19.47.54_7ae53af6.jpg>)
---

## Final Deliverable: Unique C Test

### 1. Create `unique_test.c`
```c
#include <stdint.h>
#include <stdio.h>

#ifndef USERNAME
#define USERNAME "unknown_user"
#endif

#ifndef HOSTNAME
#define HOSTNAME "unknown_host"
#endif

// 64-bit FNV-1a
static uint64_t fnv1a64(const char *s) {
    const uint64_t FNV_OFFSET = 1469598103934665603ULL;
    const uint64_t FNV_PRIME = 1099511628211ULL;
    uint64_t h = FNV_OFFSET;
    for (const unsigned char *p = (const unsigned char*)s; *p; ++p) {
        h ^= (uint64_t)(*p);
        h *= FNV_PRIME;
    }
    return h;
}

int main(void) {
    const char *user = USERNAME;
    const char *host = HOSTNAME;
    char buf[256];
    int n = snprintf(buf, sizeof(buf), "%s@%s", user, host);
    if (n <= 0) return 1;
    uint64_t uid = fnv1a64(buf);
    printf("RISC-V Uniqueness Check\n");
    printf("User: %s\n", user);
    printf("Host: %s\n", host);
    printf("UniqueID: 0x%016llx\n", (unsigned long long)uid);
#ifdef __VERSION__
    unsigned long long vlen = (unsigned long long)sizeof(__VERSION__) - 1;
    printf("GCC_VLEN: %llu\n", vlen);
#endif
    return 0;
}
```
![alt text](<WhatsApp Image 2025-08-07 at 22.25.20_b6ca6473.jpg>)
### 2. Compile with Injected Identity

```bash
echo "Username: '$(id -un)'"
echo "Hostname: '$(hostname -s)'"
```
![alt text](<WhatsApp Image 2025-08-07 at 21.56.57_dca96653.jpg>)
```bash
riscv64-unknown-elf-gcc -O2 -Wall -march=rv64imac -mabi=lp64 \
-DUSERNAME='"hitanshu"' -DHOSTNAME='"hitanshu-VirtualBox"' \
unique_test.c -o unique_test
```

### 3. Run on Spike + Proxy Kernel

```bash
spike pk ./unique_test
```

---
**Output**:-
![alt text](<WhatsApp Image 2025-08-07 at 19.47.55_0f7d11e6.jpg>)
## Conclusion
This task provided valuable hands-on experience with the bare-metal RISC-V development workflow — covering everything from toolchain setup to compiling and executing C programs on an ISA-level simulator. Successfully performing these steps on Ubuntu enhanced my understanding of open-source hardware development and low-level Linux-based toolchains.

Overall, this setup establishes a solid foundation for more advanced phases of the lab, including RTL simulation, hardware synthesis, and full SoC-level design and integration.
