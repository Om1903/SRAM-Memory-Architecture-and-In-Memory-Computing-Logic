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


