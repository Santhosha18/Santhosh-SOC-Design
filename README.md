# Digital VLSI SoC Design and planning Training
Welcome to the OpenLane workshop! In this workshop, we'll explore the complete process of designing an Application Specific Integrated Circuit (ASIC) using the OpenLane ASIC flow. We'll start with a Register Transfer Level (RTL) design and proceed through each stage of the flow, ultimately generating a Graphical Data System (GDS) file. The workshop covers all essential steps involved in this process.
## Lessons Learned
Comprehending the RTL to GDS Process
1. Complete RTL to ASIC Layout Process 
   Gained a thorough understanding of the entire process of transforming a high-level hardware description into a physical ASIC layout. Recognized the critical role of each stage, from synthesis to final sign-off.
2. Synthesis:  
   Learned how RTL is transformed into a gate-level netlist using standard cell libraries. Familiarized with various cell views, including Liberty, HDL, SPICE, and Layout.
3. Floor and Power Planning:  
   Grasped the importance of floor planning in chip partitioning and the strategic placement of I/O pads.
# Day 1
The RTL to GDSII flow is a crucial process in VLSI design that transforms an RTL description of a digital circuit into a physical layout suitable for fabrication. This flow involves several stages, including RTL synthesis, floor planning, placement, and routing, ultimately producing the GDSII file format, which encapsulates the layout data. This detailed process ensures that the final IC layout accurately represents the intended functionality while adhering to fabrication standards.

![image](https://github.com/user-attachments/assets/beac2239-2ad3-4c92-8167-11923e99df03)
# QFN-48 Chip: Package Details, Pads, Core, Die, and IPs
The VSD Squadron Board, illustrated below, features a specific focus on the enclosed region that houses the "Microprocessor." This is the component we will design using the RTL to GDS flow, transitioning from the abstract level to the final fabrication level.

![image](https://github.com/user-attachments/assets/f31e8c91-305f-4346-884a-ca50ada2f773)

# Essentials of IC Design: Components and Terminologies
![image](https://github.com/user-attachments/assets/89e77924-d8e0-4240-b68e-8206b285577c)
![image](https://github.com/user-attachments/assets/8fc58e55-ec3e-47fd-9d24-7cf6ea6174d6)
- **Core**

  The core is the central region of the chip where the essential logic circuits are located. It includes all the combinational circuits, as well as soft and hard IPs, and the interconnecting nets. This area is crucial as it contains the main functional elements that drive the chip's operations.

- **Die**

  The die is the section of the chip that encompasses the core and the IO pads. Multiple dies are patterned across a silicon wafer to maximize production efficiency. Each die contains all the necessary components for the chip to function independently once it’s separated from the wafer.

- **IO Pads**

  IO pads serve as the communication bridge between the core and the external environment. These pins allow signals to flow in and out of the chip. Surrounding the IO pads are pad cells, which form rectangular metal patches where external connections are made. The pads include input, output, and power connections, playing a critical role in the chip's interaction with other systems.

- **IPs**

  Foundry IPs are pre-designed blocks that require manual design efforts or human intervention to be defined and created, such as SRAM, ADCs, DACs, and PLLs. These IPs are integral to the chip design, providing ready-made, tested components that can be integrated into the larger design.

- **PDKs**

  PDKs act as the bridge between the foundry and design engineers. They contain a collection of files that model the fabrication process, providing crucial data for design tools used in IC creation. This includes device models, DRC (Design Rule Check), LVS (Layout Versus Schematic), physical extraction, layers, LEF (Library Exchange Format), standard cell libraries, and timing libraries. In this workshop, we use the SkyWater 130nm PDK, specifically the sky130_fd_sc_hd, which is the foundation around which OpenLANE is built.

  # Introduction to RISC-V
  **ISA:** The "Instruction Set Architecture" (ISA) is a fundamental interface between software and hardware. When we write programs in languages like C or Java, these high-level languages need to be translated into a format that a computer can understand. This is where ISA plays a crucial role. It converts the assembly language instructions into binary, the machine's native language. The RISC-V ISA, one of the latest and most advanced architectures, is designed to efficiently perform this translation process.
  
![image](https://github.com/user-attachments/assets/26174731-da34-4983-a22b-a6ae9b652eba)
# Software Applications to Hardware
In everyday scenarios, we usually interact with application software, such as apps, to communicate with hardware. But how does this interaction actually happen? Between the application software and the hardware lies a crucial layer called system software. This layer acts as a mediator, taking the commands from applications and converting them into binary language, which the hardware can understand.

The system software consists of several layers:
![image](https://github.com/user-attachments/assets/3869db1e-957f-4fb8-a612-ec0abd6a15cc)
- **Operating System (OS)**

  Beyond managing essential tasks such as input/output operations, memory management, and low-level system functions, the OS also translates application software into executable code using languages like C, C++, or Java.

- **Compiler**

  The compiler then takes this high-level code from the OS and compiles it into an instruction set, typically resulting in executable files (e.g., .exe). These instructions are specifically designed to match the hardware architecture they will run on.

- **Assembler**

  Finally, the assembler converts these executable files into binary code, which is the machine language that the hardware can understand and execute to carry out the intended operations.

# Overview of OpenLane Components for Digital ASIC Design
To Design an Open-Source Digital ASIC, Several Key Components Are Required

