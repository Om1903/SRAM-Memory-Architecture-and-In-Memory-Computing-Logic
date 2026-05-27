# SRAM-Memory-Architecture-and-In-Memory-Computing-Logic
**Introduction**

As modern workloads scale—particularly in Artificial Intelligence (AI), Machine Learning (ML), and deep neural networks—traditional computing frameworks face a severe physical bottleneck. This repository presents the design and implementation of a 6T SRAM Memory Architecture tailored for Digital In-Memory Computing (DIMC) using Cadence Virtuoso.

In conventional Von-Neumann computing architectures, the processing unit (CPU/GPU) and the memory storage unit are physically distinct. Every computation requires data to be continuously fetched from memory, transferred across internal buses to the processor, and then sent back to memory for storage.
<img width="1129" height="310" alt="image" src="https://github.com/user-attachments/assets/85102d04-bf74-4d2a-8100-cb8b3e381b00" />

**The Problem: The Von-Neumann Bottleneck**

Physical Separation of Units: Conventional computing forces a strict physical separation between the processing units (CPU/GPU) and the memory storage. This structural division demands that every single computational instruction or piece of data be continuously dragged back and forth across narrow, restrictive system buses just to perform simple operations.

<img width="850" height="441" alt="image" src="https://github.com/user-attachments/assets/77a0c428-0cc3-4d03-abbb-c89969d9acf0" />



**Digital In-Memory Computing Architecture**

Digital IMC is a computing approach where logic operations like AND, OR, XOR,addition etc are performed directly inside memory, rather than transferring data to a separate processor. Since all operations use binary values (0s and 1s), it's called digital IMC—offering high reliability, speed, and energy efficiency.

To enable this, we use SRAM as a key component because it can store weights and input data in binary form, and also allows performing bitwise operations within the memory array itself. SRAM is fast, CMOS-compatible, and ideal for repeated read/write cycles—making it perfect for implementing digital logic directly in hardware.



**SRAM 4x4 Array Peripharals and Architecture Using CMOS Technology**

**1. 6T SRAM Bitcell**

**Six-Transistor Structure**: A standard 6T SRAM cell uses six transistors to store a single bit of data. It consists of two cross-coupled inverters (4 transistors) that form a latch to lock the data in place, and two access transistors (2 transistors) to control entry to the cell.

**Static Storage**: Unlike DRAM (which uses capacitors that leak charge and need constant refreshing), an SRAM cell holds its data continuously as long as power is supplied.

<img width="670" height="343" alt="image" src="https://github.com/user-attachments/assets/1a72d3ce-a946-4293-84af-5a09967c5fb9" />



**2. Read and Write Operation in 6T Cell**

**(a)Read Operation**
**Read OperationPrecharge**: Both vertical Bit Lines (BL and BL') are initially charged up to the supply voltage (Logic 1).

**Turn On**: The Word Line (WL) is driven HIGH, opening the two access transistors.Discharge: Inside the cell, whichever node is storing a 0 will pull its connected Bit Line down toward ground. For example, if $Q = 0$, the line BL starts to discharge.

**Sensing**: The Sense Amplifier detects this tiny voltage drop on one of the Bit Lines, instantly amplifies it, and outputs the read data.

<img width="748" height="324" alt="image" src="https://github.com/user-attachments/assets/ea2549c8-2239-4d6b-8a4b-c41a63555557" />

**(b)Write Operation**

**Pre-driving the Bit Lines**: The external write drivers force the desired value onto BL and the exact opposite value onto BL'. For example, to write a 1, BL is driven to full supply voltage ($V_{DD}$) and BL' is pulled completely to Ground ($GND$).

**Enabling Access Paths**: The Word Line (WL) is driven HIGH, turning on both access transistors. This connects the strongly driven external bit lines directly to the cell's internal storage nodes ($Q$ and $Q'$).

**Overpowering the Latch**: Because the external write drivers are physically larger and electrically stronger than the cell's internal inverters, they effortlessly overwhelm the old state. The ground line on BL' drains the high node, forcing the internal feedback loop to instantly flip.

**Locking the State**: Once the cell flips to match the bit lines, the Word Line (WL) is pulled back LOW. This closes the access transistors, isolating the cell and securely locking the new data inside.

<img width="730" height="406" alt="image" src="https://github.com/user-attachments/assets/f923d123-979c-43cb-ad21-c49bd05ab1cb" />

**3. Precharge Circuit**

**Precharge & Equalization**: Utilizes a 3-PMOS network to pull both $\text{BL}$ and $\text{BLB}$ up to $V_{dd}$ and equalize their potentials.

**Read Readiness**: Prevents read disturbs and speeds up sensing margins by establishing a clean, balanced baseline before wordline activation.

<img width="690" height="469" alt="image" src="https://github.com/user-attachments/assets/f919c55b-41e1-4185-82d6-f35d3e8f3d92" />

**4. Cross Coupled Sense Amplifier**

Read Operation:

When a wordline is activated, the bitcell slightly pulls down either BL or BLB, depending on whether it stores 0 or 1

This creates a tiny imbalance between BL and BLB.

The sense amplifier, which is connected to both lines, is then enabled (using SAE).

The sense amplifier detects the data stored based on changes observed in BL and BLB value , if BL changes from 1->0 then it means data stored in bitcell is logic 0 and if BLB changes from 1->o depicts data stored was logic 1

Note - These BL and BlB were precharged initially before read operation and thus changes in these values are fed to sense amplifier .

**Why Cross Coupled Design?**

Works well even when the cell doesn’t strongly pull the bitlines (important for low-voltage or fast-access SRAM), hence High Sensitivity.

It only turns on when SAE (Sense Amplifier Enable) is high.

With SAE low; Data and Data# are pre-charge high 

<img width="1111" height="702" alt="image" src="https://github.com/user-attachments/assets/782e4504-d6f4-4d93-9448-41d450f2894e" />

**5. Write Driver**

A circuit which basically forces the data into the bitcell by enabling wr_enable control.

It also uses BL and BLB and based on their value the 1 bit data is written into the bitcell .

The circuitry works as , if BL changes from 1->0 the logic 0 will be written into the bitcell and if BLB is changed form 1->0 then logic 1 will be written.

<img width="453" height="301" alt="image" src="https://github.com/user-attachments/assets/6fdb565a-7838-476f-8d95-fb00c86a3982" />


**Overall Circuit for 1 bitcell read and write**

<img width="375" height="880" alt="image" src="https://github.com/user-attachments/assets/260eff56-d7bf-479e-82fc-352ded82e6bc" />

**Final Circuit 2*2 SRAM Array**

<img width="375" height="880" alt="image" src="https://github.com/user-attachments/assets/e88dcaba-242d-4671-99b1-fe65ab9818dc" />

