### Inception of Open-Source EDA, OpenLANE, and Sky130 PDK

---

### 💬 1. Talking to Computers

Computers understand only **electrical signals** represented by binary logic (**1s and 0s**).

To communicate with them, humans use **layers of abstraction** that gradually translate high-level concepts into hardware-understandable instructions.

🧠 **Flow of Translation:**

- High-level programs (C, Python)
    
    ↓
    
- Compiled to **Assembly code** (specific to ISA)
    
    ↓
    
- Converted to **Machine code (binary)**
    
    ↓
    
- Executed by **Logic gates & transistors**

Each level bridges the gap between **human-written logic** and **electronic hardware**, forming the fundamental communication chain of computation.

---

### ⚙️ 2. Chip and Package Fundamentals

Modern processors and SoCs are built on a small **silicon die**, later enclosed inside a **package** for protection and connectivity.

A common example is the **QFN-48 (Quad Flat No-Lead)** package with 48 electrical contacts.

🔍 **Inside the package:**

- **Die/Core** → performs computation
- **Pads** → metal terminals for input/output
- **Bond wires** → connect die pads to package leads
- **Leads** → metallic pads soldered to the PCB

From the top-down view:

**Board → Chip → Die → Core → IP**, each layer adds specific functionality.

| Term | Description |
| --- | --- |
| **Package** | Protective housing that connects silicon to PCB |
| **Die/Chip** | Actual semiconductor area fabricated using CMOS |
| **Core** | Central processing logic |
| **Pads** | Metal contacts on die for electrical connection |
| **IP Block** | Reusable functional module like UART, GPIO, or RISC-V core |

---

### 🧠 3. RISC-V Architecture

**RISC-V (Reduced Instruction Set Computer – Version 5)** is an **open-source ISA** that defines how software interacts with hardware through instructions and registers — **royalty-free and highly modular**.

⚙️ **Execution Chain:**

High-Level Code

↓

RISC-V Assembly

↓

Machine Code (Binary)

↓

Processor Hardware (Logic Gates & Transistors)

🔩 Hardware implementations (like **PicoRV32**) are written in **Verilog/VHDL**.

This RTL code is then transformed into a **physical chip** through the **RTL-to-GDSII flow**, enabling fabrication using open tools like OpenLANE and Sky130.

---

### 💻 4. From Software Applications to Hardware

Applications such as calculators or stopwatches rely on a **software-to-hardware stack** that bridges human code and physical signals.

🧩 **System Software Components:**

- **Operating System (OS)** → manages memory, I/O, and scheduling
- **Compiler** → converts high-level programs into assembly
- **Assembler** → translates assembly into binary machine code

📜 **Architecture-specific Assembly Styles:**

| Architecture | Assembly Style |
| --- | --- |
| Intel x86 | x86 Assembly |
| ARM | ARM Assembly |
| MIPS | MIPS Assembly |
| RISC-V | RISC-V Assembly |

When the binary is loaded into memory, the **processor fetches, decodes, and executes** each instruction — turning software into hardware activity.

---

### 🏗️ 5. Open-Source Digital ASIC Design Ecosystem

To build an open-source ASIC, three major components must work together:

1. 🧾 **Open-Source RTL Designs** – logical description (Verilog/VHDL)
2. 🧰 **Open-Source EDA Tools** – automate synthesis, placement, and verification
3. ⚙️ **Open-Source PDK** – defines the process technology and design rules

When all three are open, a complete **reproducible ASIC flow** can be achieved.

📘 **Examples:**

- **RTL Design Repositories:** OpenCores, LibreCores, GitHub SoC projects
- **EDA Tools:** OpenROAD, Qflow, Magic
- **PDK:** SkyWater Sky130 (130nm, released in 2020 by Google & SkyWater)

This open ecosystem democratizes chip design by removing the need for proprietary tools.

---

### 🔬 6. Importance of Sky130 Technology

Although **130 nm** is considered mature, it remains **reliable and affordable**, perfect for **IoT, embedded, and analog applications**.

📊 **Highlights:**

- Holds ~6% of global semiconductor market (~$4.5B)
- Used in **Intel Pentium 4 (3.5 GHz)** and **RISC-V CPUs** from OSU
- The open release of **Sky130 PDK** ignited the global **open-silicon movement**, making fabrication accessible to students and innovators.

---

### 🔄 7. Simplified RTL-to-GDSII Flow

This flow converts Verilog RTL into a **fabrication-ready layout (GDSII)**.

| Stage | Description |
| --- | --- |
| **Synthesis** | RTL → Gate-level netlist using standard cells |
| **Floorplanning** | Defines die/core area and power grid |
| **Placement** | Arranges cells for optimal area/timing |
| **Clock Tree Synthesis (CTS)** | Builds balanced clock distribution |
| **Routing** | Connects cells using metal interconnects |
| **Sign-off** | DRC, LVS, and STA verification before tape-out |

📑 **Key Checks:**

- ✅ **DRC:** Verifies layout constraints
- ✅ **LVS:** Matches layout with schematic
- ✅ **STA:** Ensures timing closure

Outputs include **GDSII layout, netlists, and timing/power reports** — ready for fabrication.

---

### 🧩 8. OpenLANE and Strive Chipsets

**OpenLANE** is a **fully automated RTL-to-GDSII flow** built around **OpenROAD** and integrated with the **Sky130 PDK**.

🧠 **Tool Integration Overview:**

| Function | Tool |
| --- | --- |
| Logic Synthesis | Yosys |
| Floorplan & Placement | OpenROAD / RePlAce |
| CTS | TritonCTS |
| Routing | FastRoute / TritonRoute |
| DRC Check | Magic |
| LVS Check | Netgen |
| Timing Analysis | OpenSTA |
| GDS Export & View | KLayout, Magic |

**Strive Chipsets** are open-source SoCs fabricated via **OpenLANE + Sky130**, containing RISC-V cores, SRAM, and I/O pads — serving as reference platforms for open-source design.

---

### 🗂️ 9. OpenLANE Flow and Directory Structure

The OpenLANE directory ensures organized and reproducible chip design.

```
OpenLANE/
├── designs/      →  Design folders (with config.tcl)
├── flow/         →  Automation scripts & Makefiles
├── scripts/      →  Stage-specific TCL scripts
├── pdks/         →  Installed process kits (e.g., sky130A)
├── openroad/     →  Core EDA engine
├── runs/         →  Generated results & logs
└── tools/        →  External binaries

```

🧾 **Command Flow:**

```bash
cd OpenLane/
make mount
./flow.tcl -design <design_name> -tag <run_name>

```

📁 **Generated Outputs:**

- `reports/` → timing, power, area data
- `results/` → final LEF, DEF, and GDS files
- `logs/` → step-by-step tool outputs

---

### 🧾 10. Summary

**Week 6 – Day 1** establishes the foundation of **open-source VLSI design** and connects software abstraction with silicon realization.

🪜 **Key Takeaways:**

- Understanding how computers interpret binary logic
- Differentiating between package, die, and core
- Exploring the open RISC-V ISA
- Learning about RTL, EDA, and PDK integration
- Understanding the RTL-to-GDSII pipeline and OpenLANE automation

Together with the **Sky130 PDK**, these tools make **chip design and fabrication truly open**, empowering researchers, students, and innovators worldwide 🌍.
