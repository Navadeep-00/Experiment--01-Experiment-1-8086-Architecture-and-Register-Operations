# Experiment--01-Experiment-1-8086-Architecture-and-Register-Operations
 
## Aim

To study the architecture of the 8086 microprocessor and write assembly
language programs for register-to-register data transfer, memory
storage, and exchanging two 16-bit memory values.

## Learning Outcomes

After completing this experiment, students will be able to: - Explain
the main functional units of the 8086 microprocessor. - Describe the
roles of the Bus Interface Unit (BIU) and Execution Unit (EU). - Write
8086 assembly instructions for 16-bit data transfer. - Exchange data
between two memory locations using registers.

## Software Required

-   An 8086 assembly emulator, such as emu8086 or an equivalent
    8086-compatible emulator.
-   A text editor for writing the assembly programs.

------------------------------------------------------------------------

## Part (a): 8086 Architecture and Functional Units

### Question

Explain the architecture of the 8086 microprocessor with a neat block
diagram, describing the functions of the BIU and EU.

Architecture of 8086 Microprocessor
The 8086 microprocessor is a 16-bit microprocessor developed by Intel. It has a 16-bit data bus, a 20-bit address bus, and can access up to 1 MB of memory. Its architecture is divided into two main units:
1. Bus Interface Unit (BIU)
2. Execution Unit (EU)
Block Diagram

     <img width="1112" height="712" alt="image" src="https://github.com/user-attachments/assets/1dda1320-ed83-4792-894f-dd0e70a06c67" />



Functions of BIU and EU
1. Bus Interface Unit (BIU)
- Fetches instructions from memory.
- Reads data from and writes data to memory and I/O devices.
- Contains the segment registers CS, DS, SS, and ES.
- Contains the Instruction Pointer (IP).
- Maintains a 6-byte instruction prefetch queue.
- Generates the 20-bit physical address using segment and offset addresses.

2. Execution Unit (EU)
- Decodes and executes instructions.
- Performs arithmetic and logical operations using the ALU.
- Contains general-purpose registers AX, BX, CX, and DX.
- Contains pointer and index registers such as SP, BP, SI, and DI.
- Maintains status and control flags.
- Takes instruction bytes from the BIU queue and executes them.

  
Working: The BIU fetches instructions while the EU executes previously fetched instructions. This overlapping operation improves processing speed and is called instruction pipelining.


------------------------------------------------------------------------

## Part (b): Transfer a 16-bit Value Between Registers and Store It in Memory

### Question

Write an 8086 assembly language program to transfer a 16-bit data value
from one register to another and store the result in memory.

### Algorithm

1.  Load a 16-bit value into AX.
2.  Transfer the value from AX to BX.
3.  Store the value in BX into the memory variable `RESULT`.
4.  Stop the program.

### Assembly Program

.MODEL SMALL
.STACK 100H
.DATA
RESULT DW ?

.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    MOV AX, 1234H
    MOV BX, AX
    MOV RESULT, BX

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN

### Expected Result

-   AX = `1234H`
-   BX = `1234H`
-   RESULT = `1234H`

### Explanation

`MOV BX, AX` copies the 16-bit contents of AX into BX without changing
AX. `MOV RESULT, BX` stores the contents of BX in the 16-bit memory
variable `RESULT`. The `MOV` instruction does not modify the source
operand.

------------------------------------------------------------------------

## Part (c): Exchange Two 16-bit Memory Locations Using Registers

### Question

Write an 8086 assembly language program to exchange the contents of two
16-bit memory locations using registers.

### Algorithm

1.  Load the first memory value into AX.
2.  Load the second memory value into BX.
3.  Store BX at the first memory location.
4.  Store AX at the second memory location.
5.  Stop the program.

### Assembly Program

 .MODEL SMALL
.STACK 100H
.DATA
NUM1 DW 1234H
NUM2 DW 5678H

.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    MOV AX, NUM1
    MOV BX, NUM2

    MOV NUM1, BX
    MOV NUM2, AX

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
 

### Expected Result

  Memory Variable     Before Execution   After Execution
  ----------------- ------------------ -----------------
  VALUE1                       `1111H`           `2222H`
  VALUE2                       `2222H`           `1111H`

### Explanation
The program starts by initializing the data segment using MOV AX, @DATA and MOV DS, AX. The instruction MOV AX, NUM1 loads the contents of the first memory location into register AX, and MOV BX, NUM2 loads the contents of the second memory location into register BX. Then, MOV NUM1, BX stores the value of BX in NUM1, and MOV NUM2, AX stores the value of AX in NUM2, thereby exchanging their contents. Finally, MOV AH, 4CH and INT 21H terminate the program. Thus, the contents of the two 16-bit memory locations are successfully exchanged using registers AX and BX.
  
------------------------------------------------------------------------

## Procedure

1.  Open an 8086-compatible assembler or emulator.
2.  Create a new assembly source file.
3.  Enter and assemble the program for the selected part.
4.  Correct any syntax or assembler-specific errors.
5.  Execute the program step by step or run it.
6.  Inspect the registers and memory variables.
7.  Record the observed results and compare them with the expected
    results.
## Screenshot of the results 
Part (b): Transfer a 16-bit Value Between Registers and Store It in Memory

<img width="421" height="422" alt="image" src="https://github.com/user-attachments/assets/63f9e9a7-80e5-4397-b738-0c57fc9f2773" />

Part (c): Exchange Two 16-bit Memory Locations Using Registers

<img width="426" height="425" alt="image" src="https://github.com/user-attachments/assets/50fb9c1b-eaca-46eb-967c-dd26f7a5577a" />

## Result

The 8086 architecture and the functions of the BIU and EU were studied.
The assembly programs demonstrate 16-bit register transfer with memory
storage and the exchange of two 16-bit memory values.


## Viva Voce Questions

1. What is the function of the BIU in the 8086?

Ans : BIU (Bus Interface Unit) fetches instructions from memory and handles data transfer between the processor and memory.

2. What is the role of the EU?

Ans : EU (Execution Unit) decodes and executes instructions using the ALU and registers.

3. Why does the 8086 use a 6-byte instruction queue?

Ans : It stores prefetched instructions so the CPU can execute instructions faster without waiting for memory every time.

4. What is the maximum physical memory address space of the 8086?

Ans : The 8086 can access 1 MB of memory (2²⁰ bytes).

5. What is the difference between a register and a memory variable?
Ans : - Register: Small, fast storage inside the CPU.
      - Memory variable: Data stored in the main memory (RAM).
6. Does the MOV instruction change the source operand?
Ans : No. The MOV instruction copies data from the source to the destination without changing the source.

7. Why are registers used when exchanging two memory values?
Ans : Registers temporarily hold values so that two memory values can be exchanged without losing either value.

8. What is the purpose of the DS segment register?
Ans : DS (Data Segment) stores the starting address of the data segment, which contains program variables.
 
` 
