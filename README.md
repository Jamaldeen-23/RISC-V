# RISC-V
# NASSCOM-RISC-V-based-MYTH-program
RV Day 1 - Introduction to RISC-V ISA and GNU compiler toolchain  
RV-D1SK1 - Introduction to RISC-V basic keywords  
RV_D1SK1_L1_Introduction  

RISC-V ISA is a base integer ISA and must be present in any implemenatation along with some optional extension. The RISC-V has been designed to support extensive customization and specialization which can be extended with one or more optional instruction-set extensions, but the base integer instructions cannot be redefine. The different instructions included in RISC-V are listed below.


types are

Pseudo instructions
Base integer instruction (RV64I, RV32I)
Multiply extension (RV64M)
Single and double floating point instruction (RV64F, RV64D)
Application binary instruction
Memory allocation and stack pointer
The detail of the RISC-V instructions set manual can be found here.

Each base integer set is characterized by the width of the register (XLEN) and size of the user address space. The most important advantage of RISC-V is that it is an open standard instruction which is easily available for academics and commercial purposes free of cost. The main github link of RISC-V is https://github.com/riscv which is a hub of the different repositories related to RISC-V.

# GNU compile toolchain
The GNU compile toolchain is a set of programming tools in LINUX system that can be use for compiling a code to generate certain executable program, library and debugger and whose detail can be found in 1 and 2. RISC-V is one such toolchain which supports C and C++ cross compiler. It supports two build modes: a generic ELF/Newlib toolchain and a more sophisticated Linux-ELF/glibc toolchain and here the github link for the same can be found.

To start off a c program to compile sum from 1 to n was written whose file is in the codes folder as sum1to9.c. The program is compiled using both the gcc compiler and RISC-V compiler. For normal gcc compiliation simply gcc <filename.c> is executed in the terminal generating an object file a.out and ./a.out is use to further run it.
![image](https://github.com/user-attachments/assets/41f357e0-1ef4-4179-a2b8-b4872ea530e4)

RV_D1SK1_L2_From Apps To Hardware

RV_D1SK1_L3_Detailed Description Of Course Content

This is the simple C program performing addition, multiplication and division.

![image](https://github.com/user-attachments/assets/b0db44d9-6d11-4d82-b3bd-d7221dca6506)

when it enters into the compiler, the instruction set will be looking like,

![image](https://github.com/user-attachments/assets/d90b4493-3c36-4038-9b27-c88200cd730a)

The instructions other than pseudo instructions will act on integer numbers.

![image](https://github.com/user-attachments/assets/6cc43153-e978-4d56-ad20-61102b923444)

If any CPU core has both the integer instructions and multiply extension, they are called as 'RV64IM' cpu core.

![image](https://github.com/user-attachments/assets/f190a6bb-42e4-4773-af56-b16bc77a75e3)

This is the simple C program performing floating point addition, multiplication and division.

![image](https://github.com/user-attachments/assets/2f3312d8-18eb-4b74-87ed-8bda0f0b7b80)

This is the instruction set of the above code. F-> single precision, D->Double precision.

![image](https://github.com/user-attachments/assets/684d777f-039e-47fb-ad5f-da850ff9a823)

If a cpu core executes integer, multiplication and floating operations, it is called as 'RV63IMFD' cpu core.

![image](https://github.com/user-attachments/assets/ae9dfa45-9964-4532-9f08-6b7fbb035e64)

In the below codes, some data transfer happening between the memory and the stack pointer.

![image](https://github.com/user-attachments/assets/2ff36c7b-1b18-4aaf-974b-255d793c673e)

Also we will be looking into 64 bit representation of the signed and unsigned integer and lets start with this. 

RV-D1SK2 - Labwork for RISC-V software toolchain  
RV_D1SK2_L1_C Program To Compute Sum From 1 to N  

![Screenshot from 2025-03-06 20-14-26](https://github.com/user-attachments/assets/88a8bc3e-1d00-45e5-a621-e1eb85e80b4a)


RV_D1SK2_L2_RISCV GCC compile And Disassemble

We will try to see the assemble code of the C program that we wrote. When we type this command, it will give a bunch of assembly codes.

![Screenshot from 2025-03-06 20-36-29](https://github.com/user-attachments/assets/5657c89d-807e-461d-b519-7ad81ddd16bb)


So, we will change the code to show less

There are many things shown. But, we are interested in the 'main' section, so type '/main' and click 'n'. Here, the address of the 'main' is 10184(in video) and there are 15 instructions inside the 'main' when we use the option '-o1' in the command. If we wish to count the instructions without counting one by one, subtract 101c0 and 10184 and divide the resultant by 4. Because, If we look into the instructions, it increment by 4.

![Screenshot from 2025-03-08 16-29-42](https://github.com/user-attachments/assets/b245f0ac-8599-4024-8f48-4297a362a5f0)

Now we are running the same command by replacing '-o1' by '-ofast'. Now the number of instructions will be higher or lesser.

RV_D1SK2_L3_Spike Simulation And Debug

We use './a.out' to get the output in 'c'. Now we will see what command to use to get the output in riscv. The command is 'spike pk sum1ton.o'. Now let us debug it using the command 'spike -d pk sum1ton.o'.   
pc->program counter  
We want our program to run till above the main and after that we will debug manually. To run till above the main we use the command 'until pc 0 address_of_main'. In this case(in video) it is, 'until pc 0 100b0'.  To find the contents of 'a2', we use the command 'reg 0 a2'. If we press enter, next instruction will run. And again if we run 'reg 0 a2', it gets modified. 'lui' means load upper intermediate which means, the data present in the right side of the instruction is loaded to the left side register from 12 to 31 bits.

![Screenshot from 2025-03-08 16-33-00](https://github.com/user-attachments/assets/703458e6-484d-41bc-9a2e-22e00fa24a26)


![image](https://github.com/user-attachments/assets/dd5c650a-7f45-4cdc-a996-b9c304bbaf08)

Here we are interested to know what is the value of 'sp' before running that instruction. So we quit it run from the beginning.


When we do that, 10 is subtracted from the value as shown below.

![Screenshot from 2025-03-08 17-26-49](https://github.com/user-attachments/assets/cf66daec-e7e5-46dd-bc6b-e204e4bc9cc6)

What does 'addi' will do?. it will add the source register and 'imm' and store it in the destination register.

![image](https://github.com/user-attachments/assets/6ac0a0e3-e2af-4341-8be1-3d59ac38dd98)



RV-D1SK3 - Integer number representation  
RV_D1SK3_L1_64-bit Number System For Unsigned Numbers  

![image](https://github.com/user-attachments/assets/5ace8c4f-987b-41b7-9992-2e8ff73cad9e)

4 bytes forms a word. 8 bytes(2 words) forms a double word. 32-bit data is a word, 64-bit data is a double word. These are about the unsigned positive numbers.

![image](https://github.com/user-attachments/assets/fb60d272-76db-439e-a029-df08b7e76e8f)

![image](https://github.com/user-attachments/assets/28b268f3-f6de-4183-b861-d60a5452de41)

![image](https://github.com/user-attachments/assets/e5cc2c21-0a2e-4a12-aa7a-77b2b78242d9)

![image](https://github.com/user-attachments/assets/3a16e415-e844-44c7-a870-fbc974d92d5c)

![image](https://github.com/user-attachments/assets/3b4052ca-b736-4038-a4de-80eb3c2cd704)

RV_D1SK3_L2_64-bit Number System For Signed Numbers

![image](https://github.com/user-attachments/assets/6f54cfb2-2ce0-49e2-ac0d-9974e801b862)

![image](https://github.com/user-attachments/assets/67771e46-f575-46b0-811a-04aa318cf176)

![image](https://github.com/user-attachments/assets/52065919-48d4-4843-b004-30a76ee1351c)

From this we observe that, the MSBs which have 0s are positive numbers and which have 1s are negative numbers. If we have 1 at the MSB, again we can do the inverse and add 1 to get the original number. These are called signed numbers.

![image](https://github.com/user-attachments/assets/17d0defc-fce1-4ca7-909b-bb12f19c1b6a)

![image](https://github.com/user-attachments/assets/2b5307d0-0e23-4880-92e8-86e6b9320ded)

Now let us see the range of positive and negative that can be represented using rv64 hardware. The number of positive numbers that can be represented is,

![image](https://github.com/user-attachments/assets/ed17cc57-b35a-4ef3-a100-cc7d55417b1d)

![image](https://github.com/user-attachments/assets/808bda60-1f1a-4cfc-afa2-ed10606ffb1f)

These are the important notes with respect to the integers.

![image](https://github.com/user-attachments/assets/eadd3e93-e53f-4687-b672-c22bf569c399)

Instructions which operate on these kind of numbers are called Base integer instructions.

![image](https://github.com/user-attachments/assets/64cc35e5-8c58-410f-ad5c-23c3bf14bc99)

RV_D1SK3_L3_Lab For Signed And Unsigned Numbers

![image](https://github.com/user-attachments/assets/bf80b185-55d7-4f04-b28c-91120924278b)

My works

![Screenshot from 2025-03-08 21-32-41](https://github.com/user-attachments/assets/12a41f98-3955-451d-9386-509b0c3a4d0a)

RV Day 2 - Introduction to ABI and basic verification flow  
RV-D2SK1 - Application Binary interface (ABI)  
RV_D2SK1_L1_Introduction To Application Binary Interface  

![image](https://github.com/user-attachments/assets/0505fcd3-6d1d-4e58-a478-01941ea9a6de)

![image](https://github.com/user-attachments/assets/60a853d1-da9a-4a8e-94df-49d38c153859)

If we want to present this architecture of the building to the user, the interface is appearance. Right now, the details such as plumbing are not required for the users. 

![image](https://github.com/user-attachments/assets/11e41e1c-4b46-447e-aab2-43255dd13c7b)

Similarly, in case of the computer, the interface is apperance and functionality. The details such as processors and other things are not highly required at the very beginning.

![image](https://github.com/user-attachments/assets/4598561d-7ebc-4400-a446-4ed907034e6c)

Similarly, If we want the email application program to run on the hardware, there are multiple layers inbetween and one of them is ABI. Java or C or other languages are used to build this application program. In the process of reaching the hardware, the applcation program will access the operation system through the standard libraries. The interface between the OS and the machine language is ISA(can be riscv or any other thing). This particular ISA is accessible to the operating system and to the user directly and they are called user and system ISA and user ISA. In this case the user is the Application programmer(the person who program email).  
There is also a way for the application program to access some of the hardware resources of the this OS directly, and the way it does is through the system call, which means the application programmer can directly access the registers of the riscv architecture via system calls. This interface is called ABI(also called system call interface).

![image](https://github.com/user-attachments/assets/3521f32c-d22a-456d-aea7-506d6a4eb292)

 The application programmer can access the hardware resources via registers.

 ![image](https://github.com/user-attachments/assets/c7cccb2d-9c65-40d7-a92c-b3f06347a8cb)

In riscv we have 32 registers and the width of the register is defined by a keyword called XLEN-1. Now we will get questions like, Why we need 32 registers and why 64 bits?

![image](https://github.com/user-attachments/assets/6f913e56-8f73-438f-b328-28c3fd3cafc4)

RV_D2SK1_L2_Memory Allocation For Double Words

Why there is only 32 registers?.  Now let us consider the 64 bit registers. There are 2 ways to load this 64 bit data to the registers. One is, directly we can load the data into the register. Else we can load the data in the memory and from the memory we can load it into the register.   
Let us see how to load this data to the memory and it is shown below. First byte from the LSB is stored in the below register and the other bytes follows it. This structure of the memory system is called as 'little-endian' memory addressing system and RISCV belongs to this category. There is also another memory addressing system called 'big-endian', where the Most significant Byte will be stored in the below register and the other bytes follow it. 'little-endian' memory addressing system is the reverse of 'big-endian'.

![image](https://github.com/user-attachments/assets/04845b6b-7538-4535-b9ae-9ca3d4a119e8)

The address of the below shown entire double word is m[0], the address of next double word that we load will be m[8] and so on. So, it is a multiple of 8.

![image](https://github.com/user-attachments/assets/9c65f168-97b6-42c6-823f-3104218906db)

Lets see an example of an array which holds 3 double word. And the 3rd double word is shown below, which has the LSB at m[16] and MSB at m[23]. In this case, how will we load the double word in the register?. For that, we need some basic ISA commands and will look into it.

![image](https://github.com/user-attachments/assets/0613fc61-bcb6-455f-8eff-6db9132e3f41)

RV_D2SK1_L3_Load, Add And Store Instructions With Example

Our objective is to store the below mentioned data in any one of the registers, lets take x8. If we want to access this data from the memory, we need the first address of that particular memory. So, we store the base address of this entire memory in one register(x23). Lets keep it simple by having the base address as 0. '16(x23)' means, 16 will loaded into the contents of x23 register, which means, the base address 0 is replaced by 16. 'ld' means load double word. This is how the 64-bit data will be loaded into the x8 register. 

![image](https://github.com/user-attachments/assets/261485a6-3000-432d-940a-db94ab5a08c9)

Now let us see how this command is represented inside the computer. All the instructions in the riscv are 32 bit though it is 64 bit for the registers. The bits 0 to 6 and 12 to 14 forms the opcode of the 'ld'. Opcode is a code which instructs the computer to use 'ld'. Bits 15 to 19 are used to represent the rs1. Based on the combination of 5 bits we will get the value 23(in this case). Bits 7 to 11 is used to represent rd which is 8(01000) in this case. 16 will be loaded to the bits 20 to 31.

![image](https://github.com/user-attachments/assets/6310597b-ca7e-4a05-b63e-1856f7ee8712)

Lets see another command. If we want to add the double word with the contents of x24, we need to use 'add' command.

![image](https://github.com/user-attachments/assets/8a34bf54-5881-49b5-94df-34ee21418f92)

The way we instruct the computer to execute this command is shown below. Here, opcode, funct3 and funct7 are used to form the opcode of 'add' instruction.

![image](https://github.com/user-attachments/assets/a6ad0881-9966-4c22-a45d-5689225f7f9e)

Now lets see the another command to store the data from the register to the memory and it can be done using 'sd' store doubleword command. Here, the memory locations 16 to 23 are already occupied, so lets see the free locations and store data. Since we have only 32 registers, we have to load and store the data to the memory, because memory is the place where we have space to store. 'data register rs2' is the register which stores data.

![image](https://github.com/user-attachments/assets/994c7955-6dd9-4913-9fd4-ffff60dafb2a)

Here the opcode and func3 are used to execute the 'sd'command. the offset'imm' will be split and stored in immediate[11:5] and immediate[5:0].

![image](https://github.com/user-attachments/assets/d0ab665e-67d2-49cf-959c-47eda1cf46bf)

RV_D2SK1_L4_Concluding 32-registers And Their Respective ABI Names

All the instructions that we saw will operate on integers(signed or unsigned). These instructions are called base integer instructions. Any cpu that use this 47(total) base integer instructions are called RV64I. There are multiple classifications inside the base integer instructions. The instructions which act only on registers are called R-type instructions Eg: 'add'.

![image](https://github.com/user-attachments/assets/2250f20c-c0db-4a5c-9ed7-958354e01c40)

The instructions which operate on registers and an immediate are called I-type registers Eg: 'ld'.

![image](https://github.com/user-attachments/assets/d33a3608-bf79-4d8e-9b08-34932c19a111)

The insturctions which operate on source register and immediate are called S-type registers and are used for store purpose Eg: 'sd'

![image](https://github.com/user-attachments/assets/b66b4328-155d-4584-b646-3932359d9423)

If we look into all the cases, we represent the registers using 5 bits. So, maximum we can have **2^5=32 registers**.

![image](https://github.com/user-attachments/assets/2a09c1c8-a31c-4937-9d6f-a62bf3252c11)

For each registers, an ABI name will be given through which the ABI will access the internal registers of the riscv cpu core using some system call functions.

![image](https://github.com/user-attachments/assets/4e791a2e-efad-4fdb-b13a-fca2508f1b6d)

![image](https://github.com/user-attachments/assets/7ddebe59-1895-429a-a9f0-fc8352525994)


RV-D2SK2 - Lab work using ABI function calls  
RV_D2SK2_L1_Study New Algorithm For Sum 1 to N Using ASM  

Now, using the C program we are going to make some function calls to the assembly language program in the riscv and do some computations and send the final result to the C program. The arguments will be passed to ASM using the a0 and a1 registers and returned to C program using a0 register.

![image](https://github.com/user-attachments/assets/8f96e466-53b8-4b6b-8b6a-0d1a0a391b8d)

We can use any register between a0 and a7. We initialize the registers a4 and a3 to 0. We store the count 10, which came from a1, to the register a2.

![image](https://github.com/user-attachments/assets/c951d918-dc87-4a0d-9fc6-7e67119ee350)

RV-D2SK3 - Basic verification flow using iverilog  
RV_D2SK3_L1_Lab To Run C-Program On RISC-V CPU  

Till we did the simulation. Next we will see how to run the same c program on a riscv cpu. We load the hex file of the c program to memory. We read the memory through the riscv cpu. The cpu will process the hex file and give the desired output.

![image](https://github.com/user-attachments/assets/eaef3b28-96e3-4459-b1bb-a74c4754fcc4)

The below shown is the riscv cpu that was written in verilog and testbench is also available which is shown below. Here is shown the way to read the hex file into the memory.

![image](https://github.com/user-attachments/assets/6045c197-b9d9-4c99-bae2-5531ab5f8a37)

Now let us see the standard scripts on how to create the hex files. It can found using the command 'rv32im.sh'. Here the scripts to convert to hex files, load it to the memory of the riscv, those steps are given. Finally we will get the hex files. Then we use a tool called iverilog and it will take the picorv32.v and testbench.v as the inputs and testbench.vvp file as the output.

![image](https://github.com/user-attachments/assets/4ce0947b-93fa-4edb-b3db-deca37b9aeef)

Then we run run the entire script using the command shown below and generate the hex file.

![image](https://github.com/user-attachments/assets/9ee08d58-c7bc-432f-9fef-5ce583701655)

Here is the hex file which is machine understandable.

![image](https://github.com/user-attachments/assets/561e7d53-4b97-4bd4-96c4-8ab896ed26bd)

This bitstream is loaded into the firmware.hex and firmware32.hex

![image](https://github.com/user-attachments/assets/121e6320-c0e3-40c0-ad3a-2df97ea4e90b)

![image](https://github.com/user-attachments/assets/075ec7b6-0c6f-4833-b605-6e7993a5d158)

It is loaded into the memory through the testbench.v.

![image](https://github.com/user-attachments/assets/cf9ae97e-e365-4e06-a069-cac0542e7809)

Finally we get the expected output which is highlighted below.

![image](https://github.com/user-attachments/assets/93af5da4-7c12-4a70-b2f4-1ef5be7c34a1)

![image](https://github.com/user-attachments/assets/a2113735-6c17-44e5-bdd8-45dd8c169e69)

My works
![image](https://github.com/user-attachments/assets/17b80e30-4422-45b0-8b36-54ea89a2ddf2)

picorv32.v
![image](https://github.com/user-attachments/assets/6d19107e-6cbf-4940-834b-0789285be78f)

testbench.v
![image](https://github.com/user-attachments/assets/13c26c7e-a102-4fe2-b171-952cbeda7e88)

rv32im.sh
![image](https://github.com/user-attachments/assets/db951af5-0818-4f9e-be3f-5d6eb45a95b7)

![image](https://github.com/user-attachments/assets/2eefbbbe-9f14-4b32-ac22-71a5c470898b)

firmware.hex
![image](https://github.com/user-attachments/assets/42cbe7a5-2a3e-439d-8a26-f19f834a3a0d)

firmware32.hex
![image](https://github.com/user-attachments/assets/c3dee93c-2875-47bb-a297-6aea6c05b7a1)

RV Day 3 - Digital Logic with TL-Verilog and Makerchip  
RV-D3SK1 - Combinational logic in TL-Verilog using Makerchip  
RV_D3SK1_L0_Welcome  

Makerchip introduces ground breaking capabilities for advanced Verilog design, it also makes circuit design easy fun! For this Makerchip provides free and instant access to the latest tools (both the open-source and proprietary ones) from the browser in a local system. One can easily code, compile, simulate, and debug verilog design by using the makerchip IDE platform from the browrser iteslf. Makerchip platform provides a seamless design experience as the code,log file, block diagrams, waveforms, and novel visualisation are highly organised, tightly integrated and debugging is easy.

Makerchip supports the emerging Transaction-Level Verilog or TL-Verilog standard which is a huge step forward as it allows simpler coding. As the coding becomes lesser faster development, fewer bugs, easier maintenance, and better quality silicon becomes possible. TL-Verilog adds powerful constructs for pipelines and transactions. A number of examples available in Makerchip which can be found here.

![image](https://github.com/user-attachments/assets/583b8fd0-9945-45c7-b707-dee639fcf39f)

TL(Transaction level) verilog is a language extension to verilog.

![image](https://github.com/user-attachments/assets/5cfc4d2f-603c-4fad-b945-9f0832a01e89)

![image](https://github.com/user-attachments/assets/2977b581-06b5-4a54-a7a3-389371b0bc12)

![image](https://github.com/user-attachments/assets/528757f0-c41e-40f2-8a45-a5100fe0ae6c)


RV_D3SK1_L1_Introduction To Logic Gates  

![image](https://github.com/user-attachments/assets/db579e31-5b7b-4336-999b-13fd8ad011e0)

![image](https://github.com/user-attachments/assets/93cbfaa3-1e0d-464a-a264-b5df26446b63)

![image](https://github.com/user-attachments/assets/f0b11fc9-6d40-4bbe-9cb8-6e0b7e4024c0)

![image](https://github.com/user-attachments/assets/ed53b95f-64bb-47c2-89da-b80d4bd9eb07)

These are the different notations for the gates and we will be focusing on the verilog notation.

![image](https://github.com/user-attachments/assets/1d5995f0-8910-42da-834c-01474d68582f)

RV_D3SK1_L2_Basic Mux Implementation And Introduction To Makerchip

The below shown is the ternary operator.

![image](https://github.com/user-attachments/assets/228ccea5-125c-48f2-9f66-674ace1ba51b)

![image](https://github.com/user-attachments/assets/8cc9c257-7929-4fdf-8a37-093b715faeb2)

RV_D3SK1_L3_Labs For Combinational Logic

![image](https://github.com/user-attachments/assets/01107fdc-56de-48c4-b4a0-a339ce43001b)


My screenshot
![Screenshot 2025-03-09 142806](https://github.com/user-attachments/assets/8aeb14d8-cdcf-4ba1-ad95-6ebef132ce58)

![image](https://github.com/user-attachments/assets/050dc6df-9e83-4764-80bc-9600b7563738)

Inverter 
![Screenshot 2025-03-09 144254](https://github.com/user-attachments/assets/549ffa14-0218-4f95-8a0d-0761865fdbcb)

2-input AND gate
![Screenshot 2025-03-09 144510](https://github.com/user-attachments/assets/0c36048f-c8a5-43d7-adab-8a842a4d88fa)


![image](https://github.com/user-attachments/assets/65a2fa62-4825-4c20-bd83-a54f78928237)

2 to 1 mux
![image](https://github.com/user-attachments/assets/62741aa8-8eda-4b7a-9995-3e24fda6f990)

![image](https://github.com/user-attachments/assets/86038b54-13fd-4621-b8e8-75d559ee36cc)

My work

![Screenshot 2025-03-09 193442](https://github.com/user-attachments/assets/85d7be37-33d2-4dfa-abed-944cca09b330)

RV-D3SK2 - Sequential logic  
RV_D3SK2_L1_Introduction To Sequential Logic And Counter Lab  

![image](https://github.com/user-attachments/assets/aceefa97-96e1-4cd2-89ec-9e5471c63cac)

![image](https://github.com/user-attachments/assets/10c53800-8e8f-4c01-83fa-74451c971a81)

![image](https://github.com/user-attachments/assets/da79e022-277a-404c-94dc-367e6da8795e)

![image](https://github.com/user-attachments/assets/a538cb3a-db27-446e-bd3e-2fc0cba0a8a1)

My fibnacci series
![Screenshot 2025-03-09 195849](https://github.com/user-attachments/assets/84bdabb7-bd99-47c7-9894-c23ab1c7fc36)


RV_D3SK2_L2_Sequential Calculator Lab

![image](https://github.com/user-attachments/assets/6be9c0fc-cd7c-444e-9c38-3267a25cd1c0)

![image](https://github.com/user-attachments/assets/926245cb-3950-4a7e-b3c2-4e1397fa3fa2)

RV-D3SK3 - Pipelined logic
RV_D3SK3_L1_Pipelined Logic And Re-Timing

Pipelining or timing abstract is an important feature in TL verilog as it can be implemented very easily with fewer codes as compared to system verilog which reduces bugs to a great extent. An example of the pipeling for pythogoras theorem using both TL verilog and system verilog is shown here. In TL verilog pipteling can be implemented by defining the pipeline as |calc and the different pipeline stages should be properly align and are indicated by @1, @2 and so on.

Here the first pipeline stage consists of the input followed by arithimetic operation in the second pipeline stage and finally the ouput is included 2 cycles ahead in the third pipeline stage.
![image](https://github.com/user-attachments/assets/944e010a-2443-48b7-b0ff-b57d90607685)

![image](https://github.com/user-attachments/assets/8b141a0a-5ee0-47d4-8c29-96ad3951fb38)

![image](https://github.com/user-attachments/assets/8427d262-62ef-48d4-9893-0441bca30f4f)

The same code is given in both system verilog and TL verilog. We can observe the code reduction here.

![image](https://github.com/user-attachments/assets/b3e5d2b9-479b-4978-8c66-27856bfb8a26)

Suppose we have to send the signals from one end of the die to other end, we can use pipelines like this. Here we have done Retiming and it looks pretty simple.

![image](https://github.com/user-attachments/assets/6e044f79-47b0-4895-af5c-dd871cdc4c8e)

Below code is shown for retiming in SV which seems complex than TL.

![image](https://github.com/user-attachments/assets/582a01ee-fd0d-43a4-897d-ee2486290f2e)

My work
![Screenshot 2025-03-13 070311](https://github.com/user-attachments/assets/d944f683-fe78-4500-a55d-35ece1d40a66)
![Screenshot 2025-03-13 071344](https://github.com/user-attachments/assets/100e02ab-9dd6-4f4d-be22-08b238ad7087)


RV_D3SK3_L2_Pipeline Logic Advantages And Demo In Platform

By using pipelining, we can use the high frequency clock.

![image](https://github.com/user-attachments/assets/cde5a8b4-fed8-4001-be3a-41f1d0839008)

If we look into the unpiplined form, we take the example, for aa the value is 9 and for bb, the value is c and for cc, the value if 0f, which are in hexadecimal form and obtained at the same clock pulse.

![image](https://github.com/user-attachments/assets/04ab811d-b37b-4b7a-bb5b-634794a5528c)

Now let us see the pipelined version, here, at the same clock pulse, aa is 9 and bb is c. But the output cc=0f is assigned after 2 clock pulses.

![image](https://github.com/user-attachments/assets/d2fc0adc-426f-4bac-a51d-d3066d6c4ad7)

RV_D3SK3_L3_Lab On Error Conditions Within Computation Pipeline

![image](https://github.com/user-attachments/assets/43371772-5f8b-4505-b021-b3503dde213b)

![image](https://github.com/user-attachments/assets/578f1103-1a01-401e-9853-bb8b622e3361)

![image](https://github.com/user-attachments/assets/36d913b5-2a2b-4bd9-982c-ed52bc0b6f2e)

My work
![image](https://github.com/user-attachments/assets/ea70fb0c-b13d-4c76-8ff7-80ed1103c97f)

RV_D3SK3_L4_Lab On 2-Cycle Calculator

![image](https://github.com/user-attachments/assets/1d2a08a0-d402-4b19-b7bd-dfe39ffcd385)

![image](https://github.com/user-attachments/assets/9ecb2d23-95fd-49f7-9c4e-5bce03fa8362)

My work
![cropped_image](https://github.com/user-attachments/assets/139cccea-38fe-470f-af9c-4a5ccd904c2e)


RV-D3SK4 - Validity  
RV_D3SK4_L1_Introduction To Validity And Its Advantages  

Validity concept is not exist in RTL languages. Here, '?' means 'when', so '?$valid' means, when valid.Validity is another feature in TL verilog which is asserted if a particular transactions in a pipeline is valid or true. A new scope, called “when” scope is introduced for this and it is denoted as ?$valid. This new scope has many advantages - easier design, cleaner debug, better error checking and automated clock gating. 

![image](https://github.com/user-attachments/assets/c7457a78-e3fd-4c13-a500-2fc7e2378c60)

![image](https://github.com/user-attachments/assets/0b5f9ca9-68e0-4d59-8a65-005de93bdf6b)

RV_D3SK4_L2_Lab On Validity And Valid When Condition

When the new distance is not valid, the previous distance will be holded. When the new distance is valid, it will get added to the existing distance.

![image](https://github.com/user-attachments/assets/7b65ac51-0568-4577-8abf-dac17d6d7d90)

![image](https://github.com/user-attachments/assets/2150fffc-f47c-4ab1-aea2-bd6b2a04ab59)

RV_D3SK4_L3_Lab To Compute Total Distance

![image](https://github.com/user-attachments/assets/210ab804-b546-45e6-ae55-340e47bfe037)

![image](https://github.com/user-attachments/assets/5a49158a-8ce2-4061-9b8f-a6ea04b2b4a4)

RV_D3SK4_L4_Lab on 2-cycle Calculator with Validity

![image](https://github.com/user-attachments/assets/66d18b60-cb00-4d63-a938-6b52c388cdc0)

My work
![image](https://github.com/user-attachments/assets/a5dfbf71-c5f9-4c3d-bc53-f427365b339a)

RV_D3SK4_L5_Calulator Single Value Memory Lab

![image](https://github.com/user-attachments/assets/66005591-b4cd-44bd-8a37-387e2384b409)

RV Day 3 Wrap-up  
(Bonus) RV_D3SK5_L1_Introduction To Hierarchy Concept  

![image](https://github.com/user-attachments/assets/e238322d-12b5-40a2-bd40-107bdacd9227)

![image](https://github.com/user-attachments/assets/fb901476-6e7e-45dd-b7f7-ee37e4d8ec08)

![image](https://github.com/user-attachments/assets/3c632bf1-7c92-428c-9960-592be1e4f627)

RV Day 4 - Basic RISC-V CPU micro-architecture  
RV-D4SK1 - Introduction to Simple RISC-V Micro-architecture  
RV_D4SK1_L1_Micro-architecture of Single Cycle RISC-V CPU  

The below shown is the micro architecture for the riscv implementation. The program counter is our pointer and it is pointed into the instruction memory into the instruction that we going to execute. The output of the instruction memory is the instruction. First we decode the instruction using decoder for finding what that instruction does. The adder present here compute the next pc. The addes uses the incremented pc value and the immediate offset from the decoder. Most instructions are arithmatic instructions operating on source registers. So, we have two source registers RFRD as shown in the below diagram. Here ALU is the calculator that we coded already. We also have memory Dmem, which stores the data or load the data. For storing the data, we get the source address and the immediate offset added up. The store data will write data to memory.

![image](https://github.com/user-attachments/assets/573c9c59-5dc4-4d2d-a357-01a82f2f37bf)

RV_D4SK1_L2_Starting Point Code for RISC-V Labs Part-1  

![image](https://github.com/user-attachments/assets/fb94a70c-2a53-41a3-9f71-59e9c31367c9)

RV_D4SK1_L3_Starting Point Code for RISC-V Labs Part-2

![image](https://github.com/user-attachments/assets/c4be2923-123b-4ae2-9b08-09867e75b0e2)

![image](https://github.com/user-attachments/assets/26b63ef1-16bf-441c-90b0-2661ace7fda9)

![image](https://github.com/user-attachments/assets/90247bd6-092d-419f-beba-914d483f039a)

RV-D4SK2 - Fetch and decode  
RV_D4SK2_L1_Implementation Plan and Lab for PC  


We will implement the cpu as mentioned in the below diagram.

![image](https://github.com/user-attachments/assets/2390c907-ee85-4b7f-ab9d-d84e8c6b57a3)

My work
![Screenshot 2025-03-13 100812](https://github.com/user-attachments/assets/02e54213-1e41-4387-b055-5cb5d185c106)

RV_D4SK2_L2_Lab For Instruction Fetch Logic

During the fetch stage, processors fetches the instruction from the memory to the address pointed by the program counter. The program counters holds the address of the next stage, in our case it is after 4 cycle and the instruction memory holds the set of instruction to be executed.

![image](https://github.com/user-attachments/assets/edceaafe-109a-48ae-82af-243c279d7cc8)

![image](https://github.com/user-attachments/assets/24caa7da-5b23-4db3-82c6-48ce92bd13dd)

RV_D4SK2_L3_Lab For RV Instruction Types IRSBJU Decode Logic

![image](https://github.com/user-attachments/assets/11346074-437a-4589-a3db-0318bd5cceb2)

My work
![image](https://github.com/user-attachments/assets/e0cd909a-6d45-4ed1-a416-0ebad896ae56)

RV_D4SK2_L4_Lab For Instruction Immediate Decode Logic For RV-ISBUJ

Now we will see from where the immediate value will be taken for different instructions.

For decoding a particular instruction, it is necessary that the isntruction type and format is known to the processor. The decoding is a crucial part and has to be done properly according to the given format to avoid error. There are 6 instructions type in RISC-V :

1.Register (R) type
2.Immediate (I) type
3.Store (S) type
4.Branch (B) type
5.Upper immediate (U) type
6.Jump (J) type

Following the decoding of the above, the instruction immediate decode for all the above, except the register type is added. The 6 others instruction format/fields including the opcode, 2 source register, destination register, funct3 and funct7 decode is included. Next the instruction field decode of the different instruction type is inserted to ensure that only valid registers are used. Finally the base instruction set decode for the various fields is incorporated. The instruction type and format is as shown in figure below and is sourced from here.


![image](https://github.com/user-attachments/assets/617c3b5f-0c04-4a52-a064-ece07330057c)

My work
![cropped_image (1)](https://github.com/user-attachments/assets/7db31a74-1824-4ca6-9689-7fa0cb24e0e0)

RV_D4SK2_L5_Lab To Decode other Fields of Instructions For RV-ISBUJ

![image](https://github.com/user-attachments/assets/9079c6f8-9ac8-4e90-8d0b-2cae88951f3b)

My work
![cropped_image (2)](https://github.com/user-attachments/assets/17f775d6-0d81-4851-bbef-0fa201376cbf)


RV_D4SK2_L6_Lab To Decode Instruction Field Based on Instr Type RV-ISBUJ

![image](https://github.com/user-attachments/assets/0f1a7a26-e05b-4207-88f6-09150e347c28)

My work
![cropped_image (6)](https://github.com/user-attachments/assets/a0505e81-136e-4417-9ad1-f77aee68ad49)

RV_D4SK2_L7_Lab To Decode Individual Instruction

The code "`BOGUS_USE" is used to say the computer that "it is ok, if the other signals present are not used", which is used used to avoid warings in log. It is the SV macro.  
Now we are using the instructions that are highly required for our purpose and ignoring other instructions now.

![image](https://github.com/user-attachments/assets/e6bb4561-827f-48ca-b44c-39f3dba3c4c0)

My work
![image](https://github.com/user-attachments/assets/87288a8a-ffa7-45eb-b7e3-8745a18b7dc4)

RV-D4SK3 - RISC-V control logic  
RV_D4SK3_L1_Lab For Register File Read Part1 (USE UPDATED SHELL CODE)  

The next task is to 'read from' and 'write into' the registers. In this operation, 2 read and write operation can be carried out simulatenously. The two src1_value/src2_value takes input from the two read register rf_read_data1/ rf_read_data2 and pass it on to the ALU unit. At present, ADDI and ADD is execute whose result is obtained in register rf_write_data. The figure below shows the input and output registers.



rd -> destination register  

![image](https://github.com/user-attachments/assets/e4574905-a4e9-4415-9682-5a2f69a2f41a)

![image](https://github.com/user-attachments/assets/0948859e-ba53-4118-87af-4b209d47d347)

RV_D4SK3_L2_Lab For Register File Read Part-2

Assign these two names mentioned below to the output of the register files.

![image](https://github.com/user-attachments/assets/44d69f7f-0441-4680-923e-ef5ba706e6a1)

RV_D4SK3_L3_Lab For ALU Operations For add/addi

![image](https://github.com/user-attachments/assets/3109f2fc-4d6e-4e7b-aac3-8aace8ba9241)

My work
![image](https://github.com/user-attachments/assets/a1da0d20-f056-4193-8c2c-1fbd81f33057)

RV_D4SK3_L4_Lab For Register File Write

![image](https://github.com/user-attachments/assets/e09a4a39-f02a-426b-9eba-fc21868c872f)

![image](https://github.com/user-attachments/assets/c2850f94-2479-452d-a8a7-74df4ee3e1ac)

RV_D4SK3_L5_Concept of Array And Register File Details

![image](https://github.com/user-attachments/assets/d1a67c08-7746-43c6-94f7-d642dcd3fa04)

![image](https://github.com/user-attachments/assets/f204ca94-55e1-4a3b-bd51-063834e77f56)

RV_D4SK3_L6_Lab For Implementing Branch Instructions

The next stage in the building of the RISC-V microarchitecture, is the addition of branches. Apart from immediate addition or addition, there may certain other conditions to be satisfied which requires to direct the PC to the branch target address. Now, we have simply added few branch instruction and updated the PC. 

![image](https://github.com/user-attachments/assets/17236023-6846-4028-bdd4-00bf572484e0)

My work
![image](https://github.com/user-attachments/assets/7c254f2d-a51e-4e17-b380-a3acfd84576d)

RV_D4SK3_L7_Lab For Completing Branch Instruction Implementation

![image](https://github.com/user-attachments/assets/52672ce2-d174-42c9-a111-c244bfd329da)

My work
![cropped_image (5)](https://github.com/user-attachments/assets/a0c196f1-4bde-428f-a97f-49a4e1652445)

RV_D4SK3_L8_Lab To Create Simple Testbench

![image](https://github.com/user-attachments/assets/62032b07-81a9-4e89-866c-0d754fbdf2dd)

RV Day 5 - Complete Pipelined RISC-V CPU micro-architecture  
RV-D5SK1 - Pipelining the CPU  
RV_D5SK1_L1_Introduction To Control Flow Hazard And Read After Write Hazard  

Now pipelining of the CPU core is done, which allows easy retiming and reduces functional bug to a great extent . Pipelining allows faster computaion. For pipelining as mentioned earlier we simply need to add @1, @2 and so on. The snapshot of the pipelining is as shown below. In TL verilog, another advantage is defining of pipeline in systematic order is not necessary. More inforamtion on timming abstract can be found in the IEEE paper "Timing-Abstract Circuit Design in Transaction-Level Verilog" by Steeve Hoover in makerchip platform itself or else here.

![image](https://github.com/user-attachments/assets/51a2c694-b183-4218-a9b2-834508a7c59a)

![image](https://github.com/user-attachments/assets/45dba3a4-5513-4b33-8485-88d89c35f123)

![image](https://github.com/user-attachments/assets/201cd3ce-c8e6-40da-ac34-425056c11635)

Hazards : The problems with the time. the branch control comes at @3 and it has to connected to the pc. Similarly the read operation can be performed after the write operation.

![image](https://github.com/user-attachments/assets/427e2d6b-c60f-41df-ace1-774cdae9ed88)

RV_D5SK1_L2_Lab To Create 3-Cycle Valid Signal

![image](https://github.com/user-attachments/assets/b96944f3-888c-43e0-96ac-a96277390c78)

![image](https://github.com/user-attachments/assets/5fadc762-c556-4ef2-bd15-55ac2b7e34e2)

![image](https://github.com/user-attachments/assets/8d3801d0-282a-40c9-ae81-aff13d534ef4)

![image](https://github.com/user-attachments/assets/561e9f7b-884d-45b2-92ac-38621ab31cbc)

My work
![image](https://github.com/user-attachments/assets/682622ad-999a-4bc9-a85d-47664c6c7a3d)

RV_D5SK1_L3_Lab To Code 3-Cycle RISC-V To Take Care Of Invalid Cycles

![image](https://github.com/user-attachments/assets/44ef1630-ce26-42a0-9712-ac9ba17cc4b0)

My work
![image](https://github.com/user-attachments/assets/173ee7e0-2cba-4f53-966a-ed37cd59848d)

RV_D5SK1_L4_Lab To Modify 3-Cycle RISC-V To Distribute Logic

![image](https://github.com/user-attachments/assets/60bb7899-7706-497a-80e2-7dae04dcb1f0)

RV-D5SK2 - Solutions to Pipeline Hazards  
RV_D5SK2_L1_Lab For Register File Bypass To Address Rd-After-Wr Hazard  

![image](https://github.com/user-attachments/assets/3f67fb85-e595-405e-94fd-4469b3415838)

![image](https://github.com/user-attachments/assets/02b1fbde-ce6b-48fa-a9c6-5a116a7df8e5)

RV_D5SK2_L2_Lab For Branches To Correct The Branch Target Path

![image](https://github.com/user-attachments/assets/196d4770-925e-4b51-bfce-9a47418b69aa)

![image](https://github.com/user-attachments/assets/cef3f8eb-7951-4e7e-a0af-243790f9ebf8)

![image](https://github.com/user-attachments/assets/7ee9b331-6f79-4cfc-80e4-a215f7eabd8c)

RV_D5SK2_L3_Lab To Complete Instruction Decode Except Fence, Ecall, Ebreak

![image](https://github.com/user-attachments/assets/967ccde2-e8cc-46c8-8116-251151f543f1)

My work
![image](https://github.com/user-attachments/assets/ea06ff07-c3b8-4a97-98c4-72c1f04d0a13)

RV_D5SK2_L4_Lab To Code Complete ALU

![image](https://github.com/user-attachments/assets/b9b7ac61-ae2c-4648-9288-7e7660f4b05f)

My work
![cropped_image (7)](https://github.com/user-attachments/assets/852e394e-fb60-439e-87a5-e520ff19a49b)

RV-D5SK3 - Load/Store Instructions and Completing RISC-V CPU  
RV_D5SK3_L1_Introduction To Load Store Instructions And Lab To Redirect Loads  

The load and store option is also included for which a 1 read/write data memory is added. Similar to branch instruction the load also has 3 cycle delay. For checking the functionality of load and store instructions a test bench is added and the data is on address 4 of Data Memory and loaded that value from Data Memory to r17. 



![image](https://github.com/user-attachments/assets/58454c9d-aed0-48bf-b7d8-78af4c51f0d3)

![image](https://github.com/user-attachments/assets/7bfe3d47-1835-42dd-909b-7f900f4626ae)

![image](https://github.com/user-attachments/assets/d9df2d1f-c617-406a-8cfd-bf2a54ae22ec)

![image](https://github.com/user-attachments/assets/346e1e38-57b2-4915-afe8-c71f19f07ad7)

RV_D5SK3_L2_Lab To Load Data From Memory To Register File

![image](https://github.com/user-attachments/assets/6d51d4d9-0931-4cb0-aa99-6985cc35fa9f)
