https://github.com/steveicarus/iverilog

https://www.youtube.com/watch?v=Eko86PGEoDY&t=92s
The `chipsalliance/rocket-chip` repository is a **generator for RISC-V based System-on-Chip (SoC) designs**.

Think of it as a "chip factory" in software. Instead of manually drawing circuits or writing raw Verilog, you use this generator to programmatically define the specs of a processor, and it outputs the actual hardware description (RTL) for you.

Here is a breakdown of what it actually does:

### 1. It Uses Chisel (Hardware Construction Language)

Unlike traditional hardware design where you might use Verilog or VHDL, Rocket Chip is built on **Chisel** (a language embedded in Scala). This allows you to generate hardware using programming concepts like object-oriented design, functions, and parameters.

### 2. It Generates "SoCs," Not Just Cores

While the "Rocket Core" is a specific 64-bit in-order RISC-V processor core included in the project, the repository is actually a **generator**. It connects that core to the rest of the system, including:

* **Memory Hierarchy:** L1 instruction and data caches.
* **Interconnects:** It uses "TileLink" (a bus protocol) to connect the processor to memory and peripherals.
* **Peripherals:** It can automatically include devices like debug modules, interrupt controllers, and bus adapters to communicate with the outside world (e.g., AXI/APB protocols).

### 3. It’s Highly Parameterized

This is the core "superpower" of Rocket Chip. Because it’s a generator, you can pass arguments to change the entire chip design instantly. For example, you can toggle a configuration switch in code to:

* Add more processor cores (for a multi-core chip).
* Change the size of the cache.
* Include or exclude specific floating-point units or accelerators.
* Optimize the design for area (smaller) vs. performance (faster).

### 4. It Outputs Verilog for Real Hardware

Once you run the generator with your chosen parameters, it outputs **Verilog**. This Verilog code is "synthesizable," meaning you can feed that output directly into:

* **FPGA tools:** (Like Vivado or Quartus) to program a real FPGA board to act like that custom chip.
* **ASIC flows:** (Like OpenLane or professional EDA tools) to eventually manufacture a custom silicon chip.

### Why is it significant?

It is one of the most important projects in the **open-source hardware** world. It was developed at UC Berkeley and provides a standard, industry-grade framework for academic researchers and companies to experiment with RISC-V architectures without needing to build a CPU from scratch.

If you are interested in computer architecture or open-source hardware, this is essentially the "Linux kernel" equivalent for chip design.



https://huggingface.co/blog/nvidia/nemotron-3-embed-wins-rteb
Think of **Yosys** (Yosys Open SYnthesis Suite) as the open-source compiler for hardware design. In the world of software development, a compiler takes code (like C++) and translates it into machine code (binary) that a processor can run. In digital electronics, **Yosys takes your hardware description code (like Verilog) and translates it into a structural blueprint of logic gates**.

This process is called **RTL Synthesis** (Register-Transfer Level synthesis). Here is exactly what Yosys handles and where it fits in the hardware pipeline:

---

## What Yosys Actually Does

### 1. The Core Synthesis Process

When you give Yosys a hardware design, it pushes it through a sequential pipeline:

* **Parsing & Frontend:** It reads your human-readable hardware description languages—primarily Verilog-2005, with newer plug-in extensions supporting SystemVerilog.
* **Elaboration:** It takes abstract code concepts (like `if/else` conditions, mathematical operations, or `always` blocks) and maps them into its own internal, math-friendly structural representations (multiplexers, flip-flops, and adders).
* **Logic Optimization:** It cleans up the design by finding redundant logic, simplifying equations, and optimizing paths. (It often passes the heavy lifting for this step to an interconnected tool called ABC).
* **Technology Mapping:** This is the finale. It translates those generic mathematical blocks into the actual, physical logic gates (AND, OR, NOT gates) available on your target hardware.

### 2. Formal Verification

Beyond just creating blueprints, Yosys acts as a backend engine for math-based chip verification. By converting circuits into mathematical solver formats (like SMT-LIB), it allows peripheral tools like **SymbiYosys (SBY)** to mathematically *prove* whether your hardware design functions flawlessly or has hidden bugs.

---

## Where Does it Output To?

Yosys doesn't actually physically program a chip or build a silicon wafer. Instead, it outputs a **gate-level netlist** (a text file describing every single gate and how they tie together) tailored to a specific target:

| Target Output | Companion Tool | What Happens Next |
| --- | --- | --- |
| **FPGAs** (e.g., Lattice iCE40/ECP5) | `nextpnr` | The netlist is routed and transformed into a bitstream to program a physical FPGA chip. |
| **ASICs** (Custom Silicon Chips) | `OpenLane` / `OpenROAD` | The netlist is mapped to standard silicon cell libraries to generate the layout files (`GDSII`) used by foundries. |

---

## What Yosys Can't Do

To avoid common points of confusion:

* **It is not a physical layout tool:** It handles the logical structure, not the spatial "place and route" layout of wires on a physical piece of silicon.
* **It is not a High-Level Synthesis (HLS) tool:** You can't feed it pure C or C++ code and expect a circuit; it requires hardware description languages.

Ultimately, Yosys is the foundational pillar of the modern **open-source EDA (Electronic Design Automation) ecosystem**. It broke open a market historically dominated by wildly expensive proprietary software suites from giants like Synopsys and Cadence, making chip design accessible to hobbyists, researchers, and open-source hardware enthusiasts.
