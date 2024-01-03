# VSD RISC-V Internship
## Day 1-Introduction to RISC-V ISA And GNU compiler toolchain
### Labwork for RISC-V software toolchain
Here we execute a simple c program using a text editor named __leafpad__ 

![lab1](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/fff95a87-e36d-428b-ac7b-71bfb57d7c1e)

Inorder to run the same program using RISCV compiler use the following code 
> riscv64-unknown-elf-gcc -o1 -mabi=lp64 -march=rv64i -o <filename.o> <filename.c>
