# VSD RISC-V Internship
## Day 1-Introduction to RISC-V ISA And GNU compiler toolchain
### RISC-V ISA
Unlike proprietary processor architectures, RISC-V is an open-source instruction set architecture (ISA) used for the development of custom processors targeting a variety of end applications. The royalty-free RISC-V ISA features a small core set of instructions upon which all the design’s software runs.
The different instructions included in RISC-V are listed below.

* Pseudo instructions - (For e.g- mv,li,ret etc)
  
* Base integer instruction (RV64I, RV32I)-For e.g-lui,addi etc

* Multiply extension (RV64M) -For e.g- mulw,divw etc

* Single and double floating point instruction (RV64F, RV64D) -For e.g- flw,fadd etc

* Application binary instruction

* Memory allocation and stack pointer

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
***
### Lab work using ABI functions call
In this labwork we write a `c` program which calls a function written in `assembly` language. This code is executed in RISC-V compiler.

This is the flowchart of the program

![image](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/b61f15db-c9e4-459f-a13c-6912c4fbc22e)


_C code_
```
#include <stdio.h>
extern int load(int x, int y);

int main() {

      int result = 0;
      
      int count = 9;
      
      result = load(0x0 , count+1);
      
      printf("Sum of number from 1 to %d is %d\n",count, result);

}

```

_Assembly code_
```
.section .text
.global load
.type load, @function

load:
      add a4, a0, zero
      add a2, a0, a1
      add a3, a0, zero
loop: add a4, a3, a4
      addi a3, a3, 1
      blt a3, a2, loop
      add a0, a4, zero
      ret
```
![new_algo_riscv_code](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/c8dd4890-923f-40e7-8638-50ecde35459e)


![new_algo_riscv_op](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/4d4f4717-94e1-48a5-903a-e067e17091d1)


***

This labwork show how to convert `c file` into `hex file` , storing it into memory and then executing using riscv cpu

![image](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/9a7fd181-218b-4f60-b11b-ca5f1fb61a44)

> vim picorv32.v

> vim testbench.v

![veri](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/9714940b-6bb9-4b58-a2c5-aad1e2f36e02)


![script for hex conversion](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/76006181-d46a-4fa4-92b8-6a7c1e9beeea)


![image](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/5ddcc6e2-faa3-4502-99b2-84bc0c4ba44a)

***
## CH32V003 RISC-V CPU
### Features
* QingKe 32-bit RISC-V2A processor, supporting 2 levels of interrupt nesting
* Maximum 48MHz system main frequency
* 2KB SRAM, 16KB Flash
* Power supply voltage: 3.3/5V
* Multiple low-power modes: Sleep, Standby
* Power on/off reset, programmable voltage detector
* 1 group of 1-channel general-purpose DMA controller
* 1 group of op-amp comparator
* 1 group of 10-bit ADC
* 1×16-bit advanced-control timer, 1×16-bit general-purpose timer
* 2 WDOG, 1×32-bit SysTick
* 1 USART interface, 1 group of I2C interface, 1 group of SPI interface
* 18 I/O ports, mapping an external interrupt
* 64-bit chip unique ID
* 1-wire serial debug interface (SDI)
* Package: TSSOP20, QFN20, SOP16, SOP8

### Application
__Wearable Temperature Monitor for Athletes__

The CH32V003 can be used in a versatile wearable temperature monitor for athletes, offering several benefits:

__Functionality:__

Temperature Sensing: The built-in 10-bit ADC can be connected to a temperature sensor (e.g., thermistor) worn on the athlete's skin or clothing.

Data Processing: The CH32V003 can process the raw ADC data, converting it to temperature values and calculating relevant metrics like heart rate variability based on temperature fluctuations.

Alerts & Notifications: The MCU can trigger alerts if the temperature exceeds a certain threshold, indicating potential heat stress or exertion levels requiring adjustment.

__Additional Features:__

Vibration Motor: The GPIOs can drive a vibration motor to provide tactile alerts for temperature or heart rate changes.

LED Indicators: LEDs can be connected to visually represent temperature range or alert states.


***
# VSDSQUADRON Platform IO

![image](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/27912a89-cb54-443e-a256-38a7b0a4cb82)

## LED BLINKING

### For 100 delay units

![image](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/8511289d-7bbb-4cd8-ac2e-00f475972b27)




https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/691ff161-42ea-4c2e-b7f1-0536944a8df2
***

# Controlling Servo motor using IR sensor


## Block diagram 
![image](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/2f1484f0-87f9-4e69-8c71-c6a6fba71c82)



## Circuit Setup
![image](https://github.com/prabuddh-50/somaiya-riscv/assets/142028580/2a3297fd-1a24-4fe4-9e86-04ca8f39724f)











