# VSD RISC-V Internship
## Day 1-Introduction to RISC-V ISA And GNU compiler toolchain
### Labwork for RISC-V software toolchain
Here we execute a simple c program using a text editor named __leafpad__ 

![lab1](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/fff95a87-e36d-428b-ac7b-71bfb57d7c1e)


Inorder to run the same program using RISCV compiler use the following code (used -O1 optimization)
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

Lets rerun the program using -Ofast optimization 
> riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o <filename.o> <filename.c>

![lab2_1](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/a814bb8d-6651-431b-a1ce-73082038fd53)
![lab2_2](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/b747ba65-5045-4cb3-82fd-4b6bd614a9a9)


The major difference between the -O1 & -Ofast is that -O1 is used to improve code execution speed without spending excessive compilation time or significantly increasing the size of the executable where -Ofast is a higher level of optimization that includes aggressive optimizations, potentially sacrificing some strict compliance with language standards for performance gains.







