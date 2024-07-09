# VSDSQUADRON RESEARCH INTERNSHIP 2024


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<details>
  <summary><b> Task 1:</b> The Task is to install all the required tools for this internship and run a sample C code using the RISC-V development kit </summary>
  <br>
  
  **1.Installing Oracle VM Virtual Box Manager**

  ![Oracle VM Virtual Box manager](https://github.com/nehith01/vsdsquadron_internship/blob/main/task1/1.VIRTUAL%20BOX%20INSTALLATION.png?raw=true)
  
  **2.Installing leaf pad**
  
  *Use the following command to install the leaf pad into your Ubuntu system*
  ```
sudo apt install leafpad
```

**3.Sample C code**

![sample c code](https://github.com/nehith01/vsdsquadron_internship/blob/main/task1/3.Sample%20code.png?raw=true)
After entering the sample code into the leaf pad we will save the code 

**4.To get the output for the code**

*Use the following command to get the output for the code*
```
leafpad sum1ton.c &
./a.out
```

**5.Implementing sample C code in the RISC-V kit**
 *use the following command to implement the code*
 ```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```
After the instruction is processed we will be getting the assembly code for the sample c code 

![assembly code](https://github.com/nehith01/vsdsquadron_internship/blob/main/task1/5.calculation%20of%20risv%20instructions.png?raw=true)

**6.Implementing sample C code using Fast instruction**
*Command for implementing fast instruction is*
```
risv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```

![fast instruction](https://github.com/nehith01/vsdsquadron_internship/blob/main/task1/6.fast%20instruction.png?raw=true)

</details>

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


<details>
  <summary><b> Task 2:</b> The Task is to compile the Change Dispense Wizard: Engineering a Vending Machine with Advanced Change 
     System</summary>
  <br>
  
  **Vending Machine:**
  
   An innovative vending machine technology designed to effectively handle and dispense change to clients is called the Change Dispense Wizard. When giving change, this method uses a C program to determine the best way to distribute the coins. It accepts one dollar, fifty cents, twenty-five cents, ten cents, five cents, and one penny, among other amounts.

Accepting the product pricing and the customer's payment amount is the first step in the procedure. The difference is then calculated by the program to get the overall amount of change that is needed. To minimize the overall number of coins delivered, the system determines the quantity of each coin type by iterating through each denomination, starting with the greatest value.

By ensuring that the change is returned quickly and with the fewest coins feasible, this method improves both operational effectiveness and user happiness. The system verifies that the payment is adequate and responds appropriately when there are not enough funds. The Change Dispense Wizard is a reliable and fast transaction processing solution for contemporary vending machines since it uses a simple algorithm. In addition to enhancing customer experience, this solution streamlines vending machine's internal operations, increasing their efficiency and usability.

![vending machine](https://5.imimg.com/data5/SELLER/Default/2023/4/303189661/UP/GQ/QL/95260822/snack-vending-machine.jpg)

**Program to run vending machine:**
```
#include <stdio.h>

#define NUM_DENOMINATIONS 6
int denominations[NUM_DENOMINATIONS] = {100, 50, 25, 10, 5, 1};

void calculateChange(int change, int coinCount[NUM_DENOMINATIONS]) {
    for (int i = 0; i < NUM_DENOMINATIONS; i++) {
        coinCount[i] = change / denominations[i];
        change %= denominations[i];
    }
}

int main() {
    int productPrice, amountPaid, change;
    int coinCount[NUM_DENOMINATIONS] = {0};

    printf("Enter the price of the product (in cents): ");
    scanf("%d", &productPrice);

    printf("Enter the amount paid by the customer (in cents): ");
    scanf("%d", &amountPaid);
    if (amountPaid < productPrice) {
        printf("Insufficient amount paid.\n");
        return 1;
    }
    change = amountPaid - productPrice;
    printf("Total change to be returned: %d cents\n", change);

    calculateChange(change, coinCount);

    printf("Change dispensed:");
    for (int i = 0; i < NUM_DENOMINATIONS; i++) {
        if (coinCount[i] > 0) {
            printf("%d x %d cents\n", coinCount[i], denominations[i]);
        }
    }

    return 0;
}
```
![vending machine code](https://github.com/nehith01/vsdsquadron_internship/blob/main/task2/C%20pogram%20for%20vending%20machine.png?raw=true)

**Instructions to get the output of the vending machine**

```
gcc vendmachine.c
ls -ltr
./a.out
```

*Output of the vending machine is :*

 ![output](https://github.com/nehith01/vsdsquadron_internship/blob/main/task2/output%20for%20vending%20machine.png?raw=true)

 **Implementing vending machines using RISC-V kit**
 
 *Instruction for implementing:*
 ```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o vendmachine.o vendmachine.c
ls -ltr vendmachine.o
```
*Assembly code for vending machine*
```
riscv64-unknown-elf-objdump -d vendmachine.o
```
 By running the above instruction we will be getting a large number of assembly codes
 
![assembly code](https://github.com/nehith01/vsdsquadron_internship/blob/main/task2/assembly%20code%20for%20vending%20machine.png?raw=true)

*Instruction to reduce the assembly codes*
```
riscv64-unknown-elf-objdump -d vendmachine.o | less
/main
```

![reduced code](https://github.com/nehith01/vsdsquadron_internship/blob/main/task2/reduced%20assembly%20codes.png?raw=true)

</details>


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



<details>
  <summary><b> Task 3:</b> The Task is to implement the Change Dispense Wizard: Engineering a Vending Machine with Advanced Change system using spike command and debug the program.</summary>

  <br>
    
  **Objective:**

  The main objective of the task is to run the Change Dispense Wizard: Engineering a Vending Machine with Advanced Change system program using spike command and to verify the output with gcc command and the output for both the instructions should be same. 

  We will be checking the output and assembly codes under 2 conditions one is using O1 and Ofast instruction.

  *Instruction for implementing spike function*

  ```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o vendmachine.o vendmachine.c
spike pk vendmachine.o
```
The command `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o vendmachine.o vendmachine.c` is used to run the vending machine program using gcc and to run the same program using spike the instruction is `spike pk vendmachine.o` after running the program we need to check the output for both spike and gcc . If the output are same then  the program is implemented correctly 

*Output for vending machine program using spike command:*

![output](https://github.com/nehith01/vsdsquadron_internship/blob/main/task3/spike%20output.png?raw=true)

The output should be verified with the output gcc command and the outputs are the same and verified. The next step is to debug the assembly codes for the vending machine and to debug we need to launch a debugger and the command to launch the debugger is `spike -d pk vendmachine.o` and to load the data the command is `until pc 0 100b0` by using this command the contents of the assembly code for the vending machine program.

![output](https://github.com/nehith01/vsdsquadron_internship/blob/main/task3/assembly%20code%20for%20%2001%20instruction.png?raw=true)

![output](https://github.com/nehith01/vsdsquadron_internship/blob/main/task3/assembly%20code%20for%2001%20instruction%20cont.png?raw=true)

Now we will be checking the output using Ofast command and the command for implementation is 
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o vendmachine.o vendmachine.c
spike pk vendmachine.o
```
**The output for Ofast command is:**

![output](https://github.com/nehith01/vsdsquadron_internship/blob/main/task3/assembly%20code%20for%20ofast%20instruction.png?raw=true)

![output](https://github.com/nehith01/vsdsquadron_internship/blob/main/task3/assembly%20code%20for%20ofast%20instruction%20cont.png?raw=true)


</details>



----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------




<details>
  <summary><b>Task 4:</b> The Task is to classify the given instructions set into instruction types and find the 32-bit instruction code for each instruction</summary>
  <br>

  **RISC-V:**
             An open-standard instruction set architecture (ISA) called RISC-V (Reduced Instruction Set Computing - Five) is intended for use with a variety of computing devices, including embedded systems and supercomputers. Since it is free and open source, anyone can use it without having to pay royalties or licensing costs. 


**Different types of instructions:**

 There are 6 main RISC-V instruction formats. Every format has a unique layout and is utilized for various kinds of instructions:
 
1. R - Register
2. I - Immediate
3. S - Store
4. B - Branch
5. U - Upper Immediate
6. J - Jump


![instruction](https://github.com/nehith01/vsdsquadron_internship/blob/main/task4/RISC-V%20instruction%20set%20.jpg?raw=true)
   
Let's discuss each Instruction in detail

**1.R-Type (Register) Instructions:**

- R-Type instructions are used for operations that involve only registers. They typically perform arithmetic, logical, and shift operations. In RISC-V, R-type instructions are mostly utilized for operations using registers alone. They are essential for bitwise, logical, and arithmetic operations.
  
- These instructions are essential for calculations that take place directly between registers since they don't deal with memory or immediate values. R-type instructions increase processing efficiency by carrying out addition, subtraction, logical AND, OR, XOR, and shifts using the ALU (Arithmetic Logic Unit).
  
- Pipelining in RISC-V architectures is made easier and overall speed is improved by the uniformity and simplicity of R-Type instructions. These instructions ensure a clear and succinct execution flow by relying on specified fields to determine the precise action and the registers involved.
  
- Their architecture emphasizes simplicity in line with the RISC (Reduced Instruction Set Computer) concept of high-performance instruction sets that enable the processor to compute quickly and effectively.


![R type](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/5be34375-1f42-4366-bbc2-36e79af329a6)

**Fields:**

- opcode (7 bits): Specifies the operation and format of the instruction. For R-type instructions, it is 0110011.
- rd (5 bits): Destination register.
- funct3 (3 bits): Additional opcode bits to specify the exact operation.
- rs1 (5 bits): First source register.
- rs2 (5 bits): Second source register.
- funct7 (7 bits): Additional opcode bits for further specifying the operation.

**Format:** opcode rd, rs1, rs2

**2.I-Type (Immediate) Instructions:**

- In the RISC-V architecture, I-type instructions are mostly used for operations using instantaneous values, which are constants that are integrated into the instruction itself. These instructions can load data from memory, carry out arithmetic operations, and apply instantaneous values to different types of calculations. They play a crucial role in streamlining code that often has to employ constants, allowing for effective data manipulation without the need for extra load instructions.

- I-type instructions improve efficiency and code density by eliminating the need for many instructions to complete a single job, therefore streamlining processes. Because load instructions enable data to be retrieved directly into registers from memory, they are also essential for efficient memory access. All things considered, I-Type instructions greatly increase the RISC-V instruction's adaptability and efficiency.




![I type](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/9b22d286-1645-4c15-83d0-2fcda12fb87b)

**Fields:**

- opcode (7 bits): Specifies the operation and format of the instruction.
- rd (5 bits): Destination register.
- funct3 (3 bits): Additional opcode bits to specify the exact operation.
- rs1 (5 bits): Source register.
- imm (12 bits): Immediate value.

**Format:** opcode rd, rs1, imm

**3.S-Type (Store) Instructions:**

- S-type instructions are used for storing data from a register to memory. The immediate value is split between two fields for encoding purposes. S-Type instructions in RISC-V are primarily used for storing data from a register to memory. These instructions are essential for memory operations where data needs to be written to a specific memory address. 

- The S-Type instructions work by taking the contents of a source register and storing it at a memory address computed from a base register plus an immediate offset. This immediate offset allows for flexible addressing modes, enabling access to different memory locations relative to the base address.

- The typical operations in this category include SW (Store Word), SH (Store Halfword), and SB (Store Byte), which store 32-bit, 16-bit, and 8-bit values, respectively. S-type instructions play a crucial role in efficient data handling and manipulation, ensuring that the CPU can interact with memory effectively for various computational tasks and real-world applications.

![S type](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/286e8b27-bd86-447b-bee5-c0ea30ac86c7)

**Fields:**

- opcode (7 bits): Specifies the operation and format of the instruction.
- imm[11:5] (7 bits): Upper part of the immediate value.
- rs2 (5 bits): Source register (the data to be stored).
- rs1 (5 bits): Base address register.
- funct3 (3 bits): Additional opcode bits to specify the exact operation.
- imm[4:0] (5 bits): Lower part of the immediate value.

**Format:** opcode rs2, rs1, imm

**4.B-Type (Branch) Instructions:**

- B-type instructions are used for conditional branching. The immediate value is split across several fields and is used for the branch offset. In RISC-V, conditional branching—which is necessary to create control flow in programs—is accomplished using B-type instructions. By comparing two registers, these instructions assess a condition. If the condition is satisfied, they modify the program counter (PC) to branch to a target location. 

- The development of loops, if-else statements, and other control structures necessary for dynamic and responsive programs is made possible by this branching process. B-type instructions are flexible for a range of checks, including equality, inequality, and relational comparisons because of their conditional nature.

- The efficiency and versatility of RISC-V-based systems are greatly enhanced by the efficacy of these instructions in controlling program flow, which permits complex decision-making processes inside the hardware architecture. B-type instructions are essential for managing execution routes overall.


![B type](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/5ada313f-6ea1-4c7c-bae0-3be51fa2b007)

**Fields:**

- opcode (7 bits): Specifies the operation and format of the instruction.
- imm[12] (1 bit): A most significant bit of the immediate value.
- imm[10:5] (6 bits): Bits [10:5] of the immediate value.
- rs2 (5 bits): Second source register.
- rs1 (5 bits): First source register.
- funct3 (3 bits): Additional opcode bits to specify the exact operation.
- imm[4:1] (4 bits): Bits [4:1] of the immediate value.
- imm[11] (1 bit): Bit [11] of the immediate value.


**Foarmat:** opcode rs1, rs2, imm

**5.U-Type (Upper Immediate) Instructions:**

- U-type instructions load a 20-bit immediate value into the upper 20 bits of a register Upper immediate values are handled via U-type instructions in RISC-V, which are required for operations using big constants. LUI (Load Upper Immediate) and AUIPC (Add Upper Immediate to PC) are two examples of these commands. 

- The upper 20 bits of a destination register are loaded with a 20-bit instantaneous value using U-type instructions. This is very helpful for quickly configuring huge addresses or constants.

- AUIPC adds the immediate value shifted left by 12 bits to the program counter (PC), while LUI sets a register's top 20 bits while zeroing off its lower 12. These guidelines offer a simple approach to address computations, position-independent code, and huge constant management. RISC-V guarantees effective encoding and handling of big instantaneous values by using U-type instructions.


![U type](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/24b9c405-294d-4b28-b88e-84dcf1326781)

**Fields:**

- opcode (7 bits): Specifies the operation and format of the instruction.
- rd (5 bits): Destination register.
- imm[31:12] (20 bits): Immediate value.

**Format:** opcode rd, imm

**6.J-Type (Jump) Instructions:**

- J-type instructions are used for jump operations in RISC-V. They enable modifications to the program's execution flow by performing unconditional leaps to a designated point in the code. Implementing function calls, procedure returns, and code jumps to labels all need J-type instructions. By allowing for direct jumps to code segments without the need for repeated conditional checks or loops, these instructions contribute to the creation of more modular and efficient code.

- The capacity of J-type instructions to accommodate a higher immediate value and provide a wider variety of jump locations is their primary feature. Supporting big programs where jump targets may be distant from the present instruction is critical. In conclusion, RISC-V's J-type instructions are essential for

![J type](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/be040e62-03fc-41ad-bf6b-528383fd4a9f)

**Fields:**

- opcode (7 bits): Specifies the operation and format of the instruction.
- rd (5 bits): Destination register.
- imm[20|10:1|11|19:12] (20 bits): Immediate value, with bits arranged non-contiguously for encoding purposes.

**Format:** opcode rd, imm




**The given instruction set is:**


|    Mnemonic       | Insruction              | Type    | Description               |
| ----------------- | ----------------------- | ------- | ---------------------     |
|ADD r1,r2,r3       | Addition                | R       | r1=r2+r3                  |
|SUB r3,r1,r2       | Subtraction             | R       | r3=r1-r2                  |
|AND r2,r1,r3       | AND                     | R       | r2=r1&r3                  |
|OR r8,r2,r3        | OR                      | R       | r8=r1|r3                  |
|XOR  r8,r1,r4      | XOR                     | R       | r8=r1^r4                  |
|SLT r10,r2,r4      | Set Less Than           | R       | r10=(r2 < r4 ) ? 1:0      |
|ADDI r12,r3,5      | ADD Immediate           | I       | r12=r3+5                  |
|SW r3,r1,4         | Store Word              | S       | r3=Memory[r1+4]           |
|SRL r16,r11,r2     | Shift Logical Right     | R       | r16 = r11 >> r2           |
|BNE r0,r1,20       | Branch if Not Equal     | B       | if(r0 != r1) PC += 20     |
|BEQ r0,r0,15       | Branch If Equal         | B       | if(r0 == r0) PC += 15     |
|LW r13,r11,2       | Load Word               | I       | r13 = Memory[2+r11]       |
|SLL r15,r11,r2     | Shift Logical Left      | R       | r15 = r11 << r2           |



**Finding the 32-bit instruction code for each instruction:**

**1.ADD r1,r2,r3**

  - The given instruction set belongs to the R type and all the arithmetic and logical operations will be performed in the R type, r2 and r3 are added and stored in the r1 register.

   ```
    | funct7 (7 bits) | r3 (5 bits) | r2 (5 bits) | funct3 (3 bits) | r1 (5 bits) | ADD (7 bits) |
  ```

**Fields:**

- opcode for ADD = 0110011
- funct7 = 0000000
- funct3 = 000
- r1 = 00001
- r2 = 00010 
- r3 = 00011 

*32-bit instruction code is:*

```
0000000 00011 00010 000 00001 0110011
```


**2.SUB r3,r1,r2**

- The SUB Instruction set subtracts r1 from r2 and stores the output in the r3 register.

 ```
 | funct7 (7 bits) | r2 (5 bits) | r1 (5 bits) | funct3 (3 bits) | r3 (5 bits) | SUB (7 bits) |
  ```

**Fields:**

- opcode for SUB = 0110011
- funct7 = 0100000
- funct3 = 000
- r3 = 00011 
- r1 = 00001 
- r2 = 00010 

 *32-bit Instruction code:*

 ```
0100000 00010 00001 000 00011 0110011
```

**3.AND r2,r1,r3**

- The AND instruction is performing AND Gate operation between r1 and r3 and the output is stored in the r2 register

```
 | funct7 (7 bits) | r3 (5 bits) | r1 (5 bits) | funct3 (3 bits) | r2 (5 bits) | AND (7 bits) |
```

**Fields:**

- opcode for AND = 0110011
- funct7 = 0000000
- funct3 = 111
- r2 = 00010 
- r1 = 00001 
- r3 = 00011

**32-bit Instruction code:**

```
0000000 00011 00001 111 00010 0110011
```

**4.OR r8,r2,r3**

- The OR Instruction is performing OR Gate between r2 and r3 and storing the output in the r8 register.

```
| funct7 (7 bits) | r3 (5 bits) | r1 (5 bits) | funct3 (3 bits) | r2 (5 bits) | OR (7 bits) |
```

**Fields:**

- opcode = 0110011
- funct7 = 0000000
- funct3 = 110
- r8 = 01000 
- r2 = 00010 
- r5 = 00101 

**32-bit Instruction code:**

```
0000000 00101 00010 110 01000 0110011
```


**5.XOR  r8,r1,r4**

- The XOR Instruction is performing XOR Gate between r1 and r4 and storing the output in the r8 register.


```
| funct7 (7 bits) | r3 (5 bits) | r1 (5 bits) | funct3 (3 bits) | r2 (5 bits) | XOR (7 bits) |
```

**Fields:**

- opcode = 0110011
- funct7 = 0000000
- funct3 = 100
- r8 = 01000 
- r1 = 00001 
- r4 = 00100 


**32-bit Instruction code:**

```
0000000 00100 00001 100 01000 0110011
```


**6.SLT r10,r2,r4**
- The SLT Instruction is set less than the operation and is performed between r2 and r4 and stored in r10.


```
  | funct7 (7 bits) | r3 (5 bits) | r1 (5 bits) | funct3 (3 bits) | r2 (5 bits) | SLT (7 bits) |
```

**Fields:**

- opcode = 0110011
- funct7 = 0000000
- funct3 = 010
- r10 = 01010 
- r2 = 00010 
- r4 = 00100 


**32-bit Instruction code:**

```
0000000 00100 00010 010 01010 0110011
```


**7.ADDI r12,r3,5**
- The ADDI Instruction is added immediately and the register r3 is added to 5 and stored in r12

```
opcode (7 bits) | r12 (5 bits) | funct3 (3 bits) | r3 (5 bits) | 5 (12 bits)
```


**Fields:**

- opcode = 0010011
- funct3 = 000
- r12 = 01100 
- r3 = 00011 
- 5 = 000000000101 


**32-bit Instruction code:**

```
000000000101 00011 000 01100 0010011
```

**8.SW r3,r1,r4**
- The SW store word instruction set stores the memory of r1 and r4 and stores the data in r3.

```
opcode (7 bits) | imm[4:0] (5 bits) | funct3 (3 bits) | rs1 (5 bits) | rs2 (5 bits) | imm[11:5] (7 bits)
```


**Fields:**

- opcode = 0100011
- funct3 = 010
- r3 = 00011 
- r1 = 00001 
- imm[11:5] = 0000000 (upper part of 4)
- imm[4:0] = 00100 (lower part of 4)

  
**32-bit Instruction code:**

```
0000000 00011 00001 010 00100 0100011
```

**9.SRL r16,r11,r2**
- The SRL instruction set is shifted logically right performed between r11 and r2 and the output is stored in the r16 register.

```
 | funct7 (7 bits) | r3 (5 bits) | r1 (5 bits) | funct3 (3 bits) | r2 (5 bits) | SRL (7 bits) |
```

**Fields:**

- opcode = 0110011
- funct7 = 0000000
- funct3 = 101
- r16 = 10000 
- r11 = 01011 
- r2 = 00010 


**32-bit Instruction code:**

```
0000000 00010 01011 101 10000 0110011
```

**10.BNE r0,r1,20**
- The BNE is a branch if not equal operation is performed between r1 and 20 and stored in the r0 register.

```
pcode (7 bits) | imm[11] (1 bit) | imm[4:1] (4 bits) | funct3 (3 bits) | rs1 (5 bits) | rs2 (5 bits) | imm[10:5] (6 bits) | imm[12] (1 bit)
```

**Fields:**

- opcode = 1100011
- funct3 = 001
- rs1 = 00000 
- rs2 = 00001 
- imm[12|10:5|4:1|11] = 0000010100 rearranged to 0000010 100 0

 **32-bit Instruction code:**

  ```
  0000000 00001 00000 001 00101 0000001
  ```


**11.BEQ r0,r0,15**
  - The BEQ instruction set is a branch if equal is performed between r0 and 15 and stored in the r0 register.

  ```
  pcode (7 bits) | imm[11] (1 bit) | imm[4:1] (4 bits) | funct3 (3 bits) | rs1 (5 bits) | rs2 (5 bits) | imm[10:5] (6 bits) | imm[12] (1 bit)
  ```

**Fields:**

- opcode = 1100011
- funct3 = 000
- r0 = 00000 
- r0 = 00000 
- imm[12|10:5|4:1|11] = 0000001111 rearranged to 0000001 111 0


**32-bit Instruction code:**
  
  ```
  0000000 00000 00000 000 01111 0000000
  ```


**12.LW r13,r11,2**
  - The LW is load word and 2 is stored in r11 memory and then stored in r13 register.
 
```
opcode (7 bits) | rd (5 bits) | funct3 (3 bits) | rs1 (5 bits) | imm (12 bits)
```

**Fields:**

- opcode = 0000011
- funct3 = 010
- r13 = 01101 
- r11 = 01011 
- 2 = 000000000010 


**32-bit Instruction code:**

```
000000000010 01011 010 01101 0000011
```


**13.SLL r15,r11,r2**
- The SLL is shift logically left is performed between r2 and r11 and then the data is stored in the r15 register.


 ```
  | funct7 (7 bits) | r3 (5 bits) | r2 (5 bits) | funct3 (3 bits) | r1 (5 bits) | SLL (7 bits) |
```

**Fields:**

- opcode = 0110011
- funct7 = 0000000
- funct3 = 001
- r15 = 01111 
- r11 = 01011 
- r2 = 00010 

**32-bit Instruction code:**

```
0000000 00010 01011 001 01111 0110011
```




| Instruction       | Binary Instruction Format             |
|-------------------|---------------------------------------|
|  ADD r1, r2, r3   | 0000000 00011 00010 000 00001 0110011 |
|  SUB r3, r1, r2   | 0100000 00010 00001 000 00011 0110011 |
|  AND r2, r1, r3   | 0000000 00011 00001 111 00010 0110011 | 
|  OR r8, r2, r5    | 0000000 00101 00010 110 01000 0110011 |
|  XOR r8, r1, r4   | 0000000 00100 00001 100 01000 0110011 |
|  SLT r10, r2, r4  | 0000000 00100 00010 010 01010 0110011 | 
|  ADDI r12, r3, 5  | 0000000 000101 00011 000 01100 0010011|
|  SW r3, r1, 4     | 0000000 00011 00001 010 00100 0100011 |
|  SRL r16, r11, r2 | 0000000 00010 01011 101 10000 0110011 |
|  BNE r0, r1, 20   | 000000 00001 00000 001 10100 1100011  |
|  BEQ r0, r0, 15   | 000000 00000 00000 000 01111 1100011  |
|  LW r13, r11, 2   | 0000000 000010 01011 010 01101 0000011|
|  SLL r15, r11, r2 | 0000000 00010 01011 001 01111 0110011 | 


</details>




---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



<details>
  <summary><b>Task 5:</b>The task is to generate Verilog and testbench using RISC-V and verify the functional simulation for instruction and waveform</summary>
  <br>
  
  **Steps for functional simulation:**
  1. First to run the Verilog we need a tool called iverilog to install iverilog commands are `sudo apt-get update` and `sudo apt-get install iverilog`
  2. To get the waveform we need a tool called gtkwave command is `sudo apt-get install gtkwave`
  3. Create a directory using the command `mkdir Nehith`
  4. Create files using the touch command as `touch Nehith_rv32i.v` and `touch Nehith_rv32i_tb.v`
  5. Writing Verilog code and testbench is not part of the internship we will be taking references from the repo https://github.com/vinayrayapati/rv32i/
  6. Now copy the code from the `iiitb_rv32i.v` and `iiitb_rv32i_tb.v` and paste the code in `Nehith_rv32i.v` and `Nehith_rv32i_tb.v` in leaf pad and save the file
  7. To run the code and simulate use the command `iverilog -o Nehith_rv32i Nehith_rv32i.v Nehith_rv32i_tb.v` and to get the output `./Nehith_rv32i`
  8. To get the wave from use the command `gtkwave iiitb_rv32i.vcd`


![Screenshot (79)](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/6abbacc9-cc4b-4dbe-8ec7-d1c0acfe1ea4)




![Screenshot (78)](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/b09c229a-d06b-4ec0-9f37-e7c330c78f36)

After this, it will open gtkwave and the waveforms are 

*ADD r1,r2,r3*

![ADD](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/c179cc0e-0c17-4663-ad03-61952b935ccf)

*SUB r3,r1,r2*

![SUB](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/50ab6460-502e-420e-b6a7-b4cfbbb48fee)

*AND r2,r1,r3*

![AND](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/56804d00-b0ea-41f5-939e-ec0d6020c472)

*OR r8,r2,r5*

![OR](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/fe468d74-84f0-403e-802d-9abb3d434461)


*XOR r8,r1,r4*

![OR](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/b3159607-8902-4a31-9984-8570a07fc53e)


*SLT r10,r2,r4*

![SLT](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/7fdda5d8-e20f-45bf-b145-40f508a84331)


*ADDI r122,r3,r5*


![ADDI](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/8b397efc-a522-494d-a8cd-6adea42e1028)


*SW r3,r1,r4*


![SW](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/5ec2e37b-01a1-4d19-8ce2-dc681fc96f74)

*SRL r16,r11,r2*


![SRL](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/ed6abfb5-f13b-4a98-adc5-8c61142e4f1a)


*BNE r0,r1,20*


![BNE](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/e8177df7-ea8d-4620-ad2d-7ad7d088ebe5)


*BEQ r0,r0,15*


![BEQ](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/dcf87aba-c9a0-4a7a-adc8-6f9c454a686f)


*SLL r15,r11,r2*


![SLL](https://github.com/nehith01/vsdsquadron_internship/assets/127872579/50ce3f04-dead-4453-87af-4fb01d7b7ba2)


</details>


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



<details>
  <summary><b>Task 6: </b>The task is to implement Change Dispense Wizard: Engineering a Vending Machine with Advanced Change System using RISC-V board </summary>
<br>

  **OVERVIEW:**

  The Change Dispense Wizard project involves creating a vending machine with an advanced change dispensing system. This system will calculate the change due to the customer and dispense the appropriate denominations of coins. The RISC-V board will be used to control the process.


**COMPONENTS REQUIRED:**

1. RISC-V development board 
2. Coin dispenser module (compatible with various denominations)
3. LCD module
4. Keypad for user input
5. Power supply (regulated 5V)
6. Connecting wires
7. Breadboard



**Circuit Connections:**

**RISC-V Board:**

GPIO pins for controlling peripherals
UART pins for serial communication (optional)
I2C/SPI pins for communication with display and other modules

**Coin Dispenser Module:**

Control pins connected to GPIO pins of the RISC-V board
Power pins connected to 5V and GND

**LCD Display Module:**

Data pins connected to GPIO pins of the RISC-V board
Control pins (RS, RW, E) connected to GPIO pins of the RISC-V board
Power pins connected to 5V and GND

**Keypad:**

Row and column pins connected to GPIO pins of the RISC-V board



**PIN CONNECTIONS:**


**Coin Dispenser Module:**

| Coin Dispenser | RISC-V |
| -------------- | ------ |
| CP 1           | GPIO 1 |
| CP 2           | GPIO 2 |
| CP 3           | GPIO 3 |
| Power          | 5V     |
| Ground         | GND    |


**LCD Display Module**

| LCD Module | RISC-V |
| ---------- | ------ |
| RS         | GPIO 3 |
| RW         | GPIO 4 |
| E          | GPIO 5 |
| D4         | GPIO 6 |
| D5         | GPIO 7 |
| D6         | GPIO 8 |
| D7         | GPIO 9 |
| Power      | 5V     |
| Ground     | GND    |


**Keypad:**

 | Keypad     | RISC-V   |
 | ---------- | -------- |
 | ROW 1      | GPIO 10  |
 | ROW 2      | GPIO 11  |
 | ROW 3      | GPIO 12  |
 | ROW 4      | GPIO 13  |
 | COLUMN 1   | GPIO 14  |
 | COLUMN 2   | GPIO 15  |
 | COLUMN 3   | GPIO 16  |
 | COLUMN 4   | GPIO 17  |


**How to program**

```
#include <stdio.h>
#include "lcd.h"
#include "keypad.h"
#include "coin_dispenser.h"

#define NUM_DENOMINATIONS 6
int denominations[NUM_DENOMINATIONS] = {100, 50, 25, 10, 5, 1};

void calculateChange(int change, int coinCount[NUM_DENOMINATIONS]) {
    for (int i = 0; i < NUM_DENOMINATIONS; i++) {
        coinCount[i] = change / denominations[i];
        change %= denominations[i];
    }
}

int main() {
    int productPrice, amountPaid, change;
    int coinCount[NUM_DENOMINATIONS] = {0};

    // Initialize peripherals
    lcd_init();
    keypad_init();
    coin_dispenser_init();

    // Display instructions on LCD
    lcd_print("Enter price: ");
    productPrice = keypad_read_int();

    lcd_print("Enter amount paid: ");
    amountPaid = keypad_read_int();

    if (amountPaid < productPrice) {
        lcd_print("Insufficient amount paid.");
        return 1;
    }

    change = amountPaid - productPrice;
    lcd_print("Change: ");
    lcd_print_int(change);

    calculateChange(change, coinCount);

    for (int i = 0; i < NUM_DENOMINATIONS; i++) {
        if (coinCount[i] > 0) {
            coin_dispenser_dispense(denominations[i], coinCount[i]);
        }
    }

    return 0;
}
```


</details>



