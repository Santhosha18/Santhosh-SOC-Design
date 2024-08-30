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
To Design an Open-Source Digital ASIC, Several Key Components Are Required:
![image](https://github.com/user-attachments/assets/ecdbebc3-4ae5-411c-8626-a1bb0f7278e4)
- **RTL Designs**
- **EDA Tools**
- **PDK Data**
  
  ## Key Concepts in Digital ASIC Design

- **What are RTL Designs?**

  RTL (Register-Transfer-Level) design is a critical phase in the VLSI design flow, focused on creating electronic circuits using integrated circuits (ICs). It specifies a digital circuit by describing the flow of digital signals between hardware registers and the logical operations performed on these signals.

- **What are EDA Tools?**

  EDA (Electronic Design Automation) tools are software applications used to design and verify the functionality of integrated circuits (ICs). They ensure that the IC meets the required performance and density specifications.

- **What is PDK Data?**

  PDK (Process Design Kit) is a set of files used to model a fabrication process for EDA tools during IC design. This kit includes:

- Process Design Rules:
  - DRC (Design Rule Check)
  - LVS (Layout Versus Schematic)
  - PEX (Parasitic Extraction)

- Device Models

- Digital Standard Cell Libraries

I/O Libraries
# Simplified RTL to GDS Flow

The streamlined RTL to GDSII process starts with an RTL file and, through several key stages, results in a GDSII file ready for fabrication by a foundry. The stages in this process include:

![image](https://github.com/user-attachments/assets/277c7861-5936-4887-96a9-de1aab8f3925)

    Synthesis: 
    The RTL file is converted into a circuit using components from the Standard Cell Library.
    Standard Cells in the library have a regular layout with the same height but different widths.
    Each cell has various models based on electrical, HDL, Spice, and layout (abstract and detailed) parameters.

![image](https://github.com/user-attachments/assets/5d609a73-62eb-448c-8095-0eac4e0a3fd2)

    Floor Planning & Power Planning: 
    Floor Planning: Establishes the placement of components on the chip to optimize area, including the arrangement of I/O pins, ports, and pads.
    Power Planning: Develops the power distribution network (VDD and GND) using power rings, straps, and pads, typically placed on the top metal layers to reduce resistance and delay.
  
![image](https://github.com/user-attachments/assets/45afe9d7-53fc-4ba0-9edf-88d0177103a5)

    Placement:
    Components are positioned within the specified regions defined during the floor planning stage.
    Standard Cells needed for the design are arranged within their respective cell boundaries.
    Placement occurs in two phases: Global Placement (where cell overlaps might occur) and Detailed Placement (where cells are precisely positioned according to placement rules).
    
![image](https://github.com/user-attachments/assets/b7776314-ef8f-46f3-b48e-53a4a201de93)

    CTS (Clock Tree Synthesis):
    Clock routing is done prior to signal routing to minimize clock skew, which is the variation in the arrival time of the clock signal at different destinations.
    Symmetrical tree structures like H-tree, I-tree, and X-tree are employed to reduce or eliminate clock skew.
    
![image](https://github.com/user-attachments/assets/f521c06b-df48-4ae9-b7ac-dc1fc87eeb7d)

    Routing:
    Following clock routing, signal routing is carried out using the available metal layers.
    Routing is categorized into Global Routing (which creates a routing plan based on PDK guidelines) and Detailed Routing (which performs the actual routing according to the plan).

![image](https://github.com/user-attachments/assets/48f066f4-b65a-47e7-b554-57b6027c469d)

    Sign-off:
    After routing is finished, the chip undergoes several verification steps during the sign-off phase:
    Physical Verification Checks:** Includes Design Rule Check (DRC), which verifies adherence to design rules, and Layout vs. Schematic (LVS), which ensures functional correctness against the gate-level netlist.
    Timing Checks:** Static Timing Analysis (STA) is performed to identify and address any timing violations in the design.

# Introduction to OpenLANE Detailed ASIC Design Flow

The image depicts the comprehensive ASIC design flow in OpenLane. The process starts with Design RTL, which is synthesized into an optimized gate-level netlist using Yosys and ABC. This netlist undergoes Static Timing Analysis (STA) to detect timing violations. After STA, Design for Test (DFT) is optionally applied using the

![image](https://github.com/user-attachments/assets/95ebb1d9-99eb-4395-bb59-2286da076df3)

OpenLane originated as an open-source flow for a genuine open-source tape-out experiment, developed by e-fabless. It is a platform that supports various tools such as Yosys, OpenROAD, Magic, KLlayout, and other open-source tools. OpenLane integrates and abstracts the different stages of silicon implementation. At e-fabless, there is an SoC family known as Strive. Strive represents a collection of open-source SoCs featuring Open PDK, Open RTL, and Open EDA.

![image](https://github.com/user-attachments/assets/d856c790-a03a-4af5-a0c4-f73e452f0bf5)

FAULT (for DFT) includes:

- Scan Insertion
- Automatic Test Pattern Generation (ATPG)
- Test Pattern Compaction
- Fault Coverage
- Fault Simulation

![image](https://github.com/user-attachments/assets/9f5c210e-f341-47b8-96d2-db866b5ebe20)

After DFT, the next phase is Physical Implementation, also known as Automated Place and Route (PnR), using OpenRoad.

OpenRoad (for Physical Implementation) includes:

    Floor/Power Planning
    End Decoupling Capacitors and Tap Cells Insertion
    Placement: Global and Detailed
    Post-Placement Optimization
    Clock Tree Synthesis
    Routing: Global and Detailed

During Place and Route (PnR), Logic Equivalence Checking (LEC) is essential after each design change to verify that the functionality remains consistent despite netlist modifications. Another crucial step in physical implementation is the "Insertion Script for Fake Antenna Diodes."

**Dealing with Antenna Rule Violations:** During fabrication, a metal wire segment can function as an antenna, leading to charge buildup from reactive ion etching. This accumulated charge can potentially harm transistor gates.

**Solutions:**

- **Bridging:** Adding an intermediary layer to connect the metal wire, which necessitates awareness by the router.
![image](https://github.com/user-attachments/assets/7fa9fccb-a283-4eff-9d64-587cfa8748e0)

**Solutions:**

- **Add Antenna Diode Cell:** Integrate an antenna diode to dissipate accumulated charges. Antenna diodes are provided by the Standard Cell Library (SCL). For preventive measures, insert a fake antenna diode next to each cell input after placement. Run the Antenna Checker (Magic) on the routed layout. If the checker reports a violation at a cell input pin, replace the fake diode with a real one.

- **Physical Verification:** Conduct final physical verification, which includes:
  - **DRC (Design Rule Checking):** Performed using MAGIC.
  - **LVS (Layout Versus Schematic):** Conducted using MAGIC and Netgen by comparing the extracted SPICE netlist from MAGIC with the Verilog netlist.
  - **STA (Static Timing Analysis):** To identify and address any timing violations in the design.
![image](https://github.com/user-attachments/assets/19e378d1-bfbc-4684-acd2-c6dbd9c0b142)

# RTL2GDS OpenLANE ASIC Flow Practical implementation

## Day1 Labs

![image](https://github.com/user-attachments/assets/6019a93e-802a-41fb-965d-7bd5c23ac70d)

### Understanding the Use of Various Linux Commands

- **pwd:** Displays the present working directory and its path.

- **cd:** Allows navigation through directories, both forward and backward.

- **ls:** Lists all subdirectories and files in the current directory.

- **mkdir:** Creates a new directory.

- **rmdir:** Deletes an existing directory.

- **rm:** Deletes files.

- **help:** Provides information about the usage of any command.

- **clear:** Clears the terminal screen.


![fstvsd](https://github.com/user-attachments/assets/208fa8a9-6dc1-4596-8aee-7773e1d2379c)

Key Files and Directories:

    libs.ref`: Contains design libraries, including:
      lef: Library Exchange Format files that describe cell layouts.
      lib: Liberty files used for timing and power analysis.
      gds: GDSII files with the graphical layout of the cells.
      verilog: Verilog models of the cells.

    libs.tech`: Includes technology files specific to various EDA tools:
      magic: Technology files for Magic.
      klayout: Technology files and layer properties for KLayout.
      ngspice: SPICE models for circuit simulation.
      openroad: Files used in the OpenROAD flow.
      drc: Design Rule Check files.
      lvs: Layout Versus Schematic check files.
      pex: Parasitic Extraction files.
      
![commands vdg](https://github.com/user-attachments/assets/5a166fa7-5de7-478a-9aa2-60e2ccb43ba9)

To run in interactive mode (step-by-step mode):
      
    bash-4.2$ ./flow.tcl -interactive
Design step without interactive mode.
![Design step without interactive mode](https://github.com/user-attachments/assets/7c891f7b-e23d-48c5-a3d6-54e4681606c8)

    
- Package import and check

      % package require openlane
- Prepare design

      % prep -design picorv32a
  
  ![package with 0 9](https://github.com/user-attachments/assets/0c5bbb65-281a-4eb8-a155-6851333f4101)

After the preparation is complete, a new directory named with the current date will be created within the "runs" folder. This directory will include all the required subdirectories for storing results, reports, and other pertinent data.

![files created with dates](https://github.com/user-attachments/assets/8735674b-3d36-425a-a15d-6578e5509cbf)

![files in fold with date](https://github.com/user-attachments/assets/5b62588c-03a4-426d-a701-fa11c77c1af5)

The preparation step involves the following actions for the PicoRV32A design within the OpenLane flow:

 Directory Structure Setup:
- A new directory structure is created to organize design files, including subdirectories for various components (e.g., results, reports).

 LEF Merging:
- The technology LEF (.tlef) and cell LEF (.lef) files are combined into a unified format. The technology LEF provides layer information (such as metal layers), while the cell LEF includes cell information.

 Design Placement:
- All design-related files are organized and placed under the `designs` directory to ensure accessibility and proper organization for subsequent steps.

Synthesis 

    % run_synthesis

![run synthesis](https://github.com/user-attachments/assets/c23d7e38-3dad-4d69-85b1-3f9dd0049ee6)

![synthesis pic](https://github.com/user-attachments/assets/f83000ce-13cb-4199-957a-46354b9ecf81)

![synthesisprint2](https://github.com/user-attachments/assets/cb52db2f-9fe3-4432-b601-c51584fb447a)

Synthesis Map
![synthesismap](https://github.com/user-attachments/assets/51d72d2d-5214-4d77-a64b-bc1ea0f249e2)

Synthsised Netlist
![synthsised netlist](https://github.com/user-attachments/assets/b16c280a-17f4-4cf5-b30f-7f4d6956aef8)

### Calculate the Flop Ratio (FAL)

1. **Determine the Total Number of Flip-Flops (D):** Count the total number of flip-flops in the design.

2. **Determine the Total Number of Cells:** Count the total number of cells in the design, including all types of cells such as logic gates, flip-flops, and other standard cells.

3. **Apply the Formula:**

  $$
\text{FAL (Flop Ratio)} = \frac{\text{Total Number of Flip-Flops (D)}}{\text{Total Number of Cells}}
$$

4. **Perform the Calculation:** Substitute the values for the total number of flip-flops and the total number of cells into the formula to compute the flop ratio.

5. **Interpret the Result:** The flop ratio represents the proportion of flip-flops relative to the total number of cells. A higher ratio indicates a greater presence of flip-flops in the design.

![Screenshot 2024-08-25 225500](https://github.com/user-attachments/assets/0fb5e60c-1922-46ee-9a35-59d02d28e9c1)

# Day 2

## Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells

Chip FloorPlanning Considerations

![image](https://github.com/user-attachments/assets/aab5f79f-3631-4005-a5af-db3fc51fc9df)

### Utilization Factor and Aspect Ratio

To determine the Utilization Factor and Aspect Ratio, it is essential to define the height and width of both the core and die areas.

**Core Area:**
- The core is the region of the chip designated for placing all the logic cells and components. It contains the actual logic of the chip.

**Die Area:**
- The die area surrounds the core and is used for placing I/O-related components and other peripheral elements.

**Core Area Dimensions:**
- The height and width of the core area are determined by the netlist of the design, which specifies the number and arrangement of components needed to implement the logic.

**Die Area Dimensions:**
- The height and width of the die area depend on the dimensions of the core area, as it must accommodate the core plus additional space for I/O and other components.

![image](https://github.com/user-attachments/assets/e842f0b5-e8fc-47e6-8a74-efb8c62b679d)

For instance, consider a netlist with two logic gates and two flip-flops, each occupying an area of 1 square unit. The netlist consists of 4 elements, so the minimum total area required for the core area would be 4 square units.

![image](https://github.com/user-attachments/assets/60b4abfb-67ee-4ae5-9c27-03e7fcda7bdb)

![image](https://github.com/user-attachments/assets/34eec1f7-f4d7-4d71-afa0-adf446400ddd)

### Utilization Factor:
The Utilization Factor is defined as the ratio of the core area occupied by the netlist to the total core area. For an effective FloorPlan, the Utilization Factor should not be '1'. If the Utilization Factor is '1', it indicates that the core area is fully occupied with no additional space for extra logic, which is indicative of a poor FloorPlan.








