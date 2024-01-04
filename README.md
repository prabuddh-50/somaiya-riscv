# VSD RISC-V Internship
## Day 1-Introduction to RISC-V ISA And GNU compiler toolchain
### RISC-V ISA
Unlike proprietary processor architectures, RISC-V is an open-source instruction set architecture (ISA) used for the development of custom processors targeting a variety of end applications. The royalty-free RISC-V ISA features a small core set of instructions upon which all the design’s software runs.
The different instructions included in RISC-V are listed below.

-Pseudo instructions - For e.g- mv,li,ret etc
-Base integer instruction (RV64I, RV32I)-For e.g-lui,addi etc
Multiply extension (RV64M) -For e.g- mulw,divw etc
Single and double floating point instruction (RV64F, RV64D) -For e.g- flw,fadd etc
Application binary instruction
Memory allocation and stack pointer
### Labwork for RISC-V software toolchain
Here we execute a simple c program using a text editor named __leafpad__ 

![lab1](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/fff95a87-e36d-428b-ac7b-71bfb57d7c1e)


Inorder to run the same program using RISCV compiler use the following code __(used -O1 optimization)__
> riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o <filename.o> <filename.c>

The command (ls -ltr object_file) would list the contents of the "object" directory and the "file" directory in a detailed and time-reversed order.

> ls -ltr <filename.o>

![lab_2](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/48560378-6904-46cf-884d-a7e82666cd9b)

Inorder to view the disassembled object file use the command
> riscv64-unknown-elf-objdump -d <filename.o>

To view less and main function of the program
```
riscv64-unknown-elf-objdump <object file> -d <object filename.o> | less
 /main
 n 
```

![lab2](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/39ef8f9e-974d-4c9b-8c28-cb933c54c658)
Above image show the assembly level transformation of the c program



Lets rerun the program using __-Ofast optimization__ 
> riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o <filename.o> <filename.c>

![lab2_1](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/a814bb8d-6651-431b-a1ce-73082038fd53)
![lab2_2](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/b747ba65-5045-4cb3-82fd-4b6bd614a9a9)


The major difference between the -O1 & -Ofast is that -O1 is used to improve code execution speed without spending excessive compilation time or significantly increasing the size of the executable where -Ofast is a higher level of optimization that includes aggressive optimizations, potentially sacrificing some strict compliance with language standards for performance gains.
***

# Day 2- Introduction to Application Binary Interface And Basic error flow

## Application Binary Interface

The Application Binary Interface (ABI) is a set of rules and conventions that define how binary programs interact with each other and with the operating system at the binary level. In other words, the ABI specifies the low-level details of how functions are called, how parameters are passed, how data is structured in memory, and other aspects that enable different parts of a program or different programs to work together.


![abi2](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/7d006a23-e0cd-4af9-a3eb-dd8c76d397d8)

### base integer instruction examples

![image](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/40798b85-c784-4759-99a3-26e008a888ae)

1. __Load doubleword__ (type i)
   
   `ld rd, imm12(rs1)`
   
The ld rd, imm12(rs1) instruction loads a 64-bit value from memory into the destination register rd. The effective memory address is calculated by adding the signed immediate value imm12 to the value in the base register rs1.

2. __Addition__ (type r)

   `add rd, rs1, rs2`

The add rd, rs1, rs2 instruction adds the values in registers rs1 and rs2 and stores the result in register rd. Mathematically, it can be represented as rd = rs1 + rs2.

4. __Store doubleword__ (type s)

   `sd rs2, imm12(rs1)`

The sd rs2, imm12(rs1) instruction stores a 64-bit value from the source register rs2 into memory. The effective memory address is calculated by adding the signed immediate value imm12 to the value in the base register rs1







