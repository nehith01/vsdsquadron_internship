# VSDSQUADRON RESEARCH INTERNSHIP 2024
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

Now we will be checking the output using Ofast command and the command for implementing is 
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o vendmachine.o vendmachine.c
spike pk vendmachine.o
```
**The output for Ofast command is:**

![output](https://github.com/nehith01/vsdsquadron_internship/blob/main/task3/assembly%20code%20for%20ofast%20instruction.png?raw=true)

![output](https://github.com/nehith01/vsdsquadron_internship/blob/main/task3/assembly%20code%20for%20ofast%20instruction%20cont.png?raw=true)


</details>
