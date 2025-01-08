## VeeR EH1 RISC-V Quick Start Guide
Use VMware Workstation Pro 17 + Ubuntu 22.04.5 LTS
#### Install Verilator 
https://verilator.org/guide/latest/install.html
#### Clone the tool chain repo
`git clone https://github.com/riscv-collab/riscv-gnu-toolchain`
#### Install toolchain prerequisites 
   `sudo apt-get install autoconf automake autotools-dev curl python3 python3-pip python3-tomli libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev ninja-build git cmake libglib2.0-dev libslirp-dev`
#### Build the Newlib cross-compiler to get elf-gcc
   **The completed build command is `./configure --prefix=/opt/riscv --with-arch=rv32imc_zicsr --with-abi=ilp32`**
   `./configure --prefix=/opt/riscv`,then `make` (costs long time). 
   
   After many experiments, the only way is using RISCV32 tags `--with-arch=rv32imc_zicsr --with-abi=ilp32` when build the toolschain.
#### Use VeeR EH1
   1. `git clone https://github.com/chipsalliance/Cores-VeeR-EH1`
   2. `export PATH=/opt/riscv/bin:$PATH`, change the path of your RISC-V toolchain path if needed, and use `-v` to check
   3. Modify the `prefix`  to `riscv32-unknown-elf` (in L36)
   4. Modify `CFLAGS += "-std=c++11"` to `CFLAGS += "-std=c++14"` (in L77)
   5. Setup RV_ROOT and `make -f $RV_ROOT/tools/Makefile`
### Other
1. extension `zicsr' required, mentioned in https://github.com/chipsalliance/Cores-VeeR-EH1/issues/125
2. Hit max cycle count (10000000) .. stopping, mentioned in https://github.com/chipsalliance/Cores-VeeR-EH1/issues/128
   
