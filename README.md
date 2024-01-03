# VSD RISC-V Internship
## Day 1-Introduction to RISC-V ISA And GNU compiler toolchain
### Labwork for RISC-V software toolchain
Here we execute a simple c program using a text editor named __leafpad__ 

![lab1](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/fff95a87-e36d-428b-ac7b-71bfb57d7c1e)


Inorder to run the same program using RISCV compiler use the following code 
> riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o <filename.o> <filename.c>
The command (ls -ltr object_file) would list the contents of the "object" directory and the "file" directory in a detailed and time-reversed order.
> ls -ltr <filename.o>

![lab_2](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/48560378-6904-46cf-884d-a7e82666cd9b)

Inorder to view the disassembled object file use the command
> riscv64-unknown-elf-objdump -d <filename.o>
To view less and main function of the program
``` riscv64-unknown-elf-objdump <object file> -d <object filename.o> | less
/main
n ```


