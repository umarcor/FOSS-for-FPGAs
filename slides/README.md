<!-- .slide: data-background="#145A32" -->

# FOSS for FPGA development

[rodrigomelo9.github.io/FOSS-for-FPGAs](https://rodrigomelo9.github.io/FOSS-for-FPGAs/)

Rodrigo A. Melo

(joint work with Unai Martinez-Corral)

[Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/)

---
<!-- ###################################################################### -->
## Outline
<!-- ###################################################################### -->

* [Introduction](#/2)
* [Work environment](#/5)
* [Simulation](#/12)
* [Testing and Verification](#/16)
* [Implementation](#/23)
* [Others](#/30)
* [Open Hardware](#/35)
* [Final words](#/41)

---
<!-- ###################################################################### -->
## Introduction
<!-- .slide: data-background="#581845" -->
<!-- ###################################################################### -->

[⌂](#/1)

---

### What is FOSS?

* Free/Libre and/or Open Source (you can access the source code) Software (programs).
* Anyone is freely licensed to USE, COPY, STUDY, and CHANGE the software.

|   |   |   |   |   |
|---|---|---|---|---|
| ![GPL3](images/licenses/gpl3.png) | ![Creative Commons](images/licenses/cc.png) | ![BSD](images/licenses/bsd.png) | ![Apache](images/licenses/apache.png) | ![MIT](images/licenses/mit.png) |
|   |   |   |   |   |

---

### Why use FOSS?

* **GENERAL**
  * Personal control, customization and freedom
  * Privacy and security
  * Low or no costs (solutions and support)
  * Quality, collaboration and efficiency
  * Flexibility and open-standars adherence
  * Innovation
* **SPECIFIC**
  * Vendor-independence
  * Lightweight (size and speed)

---
<!-- ###################################################################### -->
## Work environment
<!-- .slide: data-background="#581845" -->
<!-- ###################################################################### -->

[⌂](#/1)

---

### Command-line

* Aka shell, terminal, console, bash...
* Most projects provide a CLI.
* Common on Linux/Unix distributions.
* On Windows:
  * [MSYS2](https://www.msys2.org/) ([hdl.github.io/MINGW-packages](https://hdl.github.io/MINGW-packages/)).
  * Windows Subsytem for Linux (WSL).

---

### Git

* A distributed version control system.
* Created in 2005 by Linus Torvalds, for the development of the Linux kernel.
* De facto standard for FOSS projects.
* Allows dealing with a software repository and managing versions in multi-user workflows.

|   |   |   |
|---|---|---|
| ![Git](images/git/git.png) | ![GitHub](images/git/github.png) | ![GitLab](images/git/gitlab.png) |
|   |   |   |

----

#### Commands

```bash
git init
git clone <REPOSITORY>
```

```bash
git log <NONE_OR_FILEs_OR_PATHs>
git diff <NONE_OR_FILEs_OR_PATHs>
git status <NONE_OR_FILEs_OR_PATHs>
```

```bash
git add <DOT_OR_FILEs>
git commit <NONE_OR_FILEs_OR_PATHs>
git push
git pull
```

```bash
git checkout -b <NEW_BRANCH>
git checkout <BRANCH>
```

[try.github.io: Resources to learn Git](https://try.github.io/)

----

#### Clone the repository of this presentation

```bash
git clone https://github.com/rodrigomelo9/FOSS-for-FPGAs.git
```

---

### Docker

OS-level virtualization to deliver software in packages called **containers**.

![Docker](images/diagrams/docker.png)

Containers are isolated one from another and bundle their own software, libraries and configuration files.

----

#### hdl/containers

[hdl.github.io/containers](https://hdl.github.io/containers/)

* `hdlc/sim:osvb` (GHDL, Verilator, cocotb, OSVVM and VUnit)
* `hdlc/impl` (nextpnr-ice40, nextpnr-ecp5, nextpnr-generic, icestorm and prjtrellis)
* `hdlc/prog` (icestorm, openocd)

----

#### Examples

```bash
$ docker run --rm hdlc/sim:osvb ghdl -v
GHDL 2.0.0-dev (v1.0.0-252-gc14fc372) [Dunoon edition]
 Compiled with GNAT Version: 8.3.0
 llvm code generator
Written by Tristan Gingold.
```

```bash
$ docker run --rm hdlc/impl yosys --version
Yosys 0.9+4052 (git sha1 5c1e6a0e, clang 7.0.1-8+deb10u2 -fPIC -Os)
```

---

### Continuous Integration/Delivery/Deployment (CI/CD)

Automatically executing actions based on repository events (push, merge, cron, etc).

* **Integration:** run linters, unit and/or integration tests, Hardware-in-the loop simulation.
* **Delivery:** build binaries, documentation, packages, etc.
* **Deployment:** build and install in production.

---

### Make

* A build automation tool: a Makefile contains a set of directives (targets, dependencies and rules) which are used by `make` for generating a target/goal.
* It works upon the principle that files only need to be recreated if their dependencies are newer than the file being re/created.
* There are newer alternatives (such as CMake, Scons, Ninja, etc.), but `make` is the most used automation tool in the FPGA ecosystem.

---

### Python

* An interpreted, high-level and general-purpose programming language.
* One of the most used and fastest growing languages in all fields, especially in scientific computing and Machine/Deep Learning.
* Many of its libraries are written in C/C++ (performance).
* Most FOSS FPGA tools are written in Python, or C/C++ with a Python binding/wrapper.
* There are several HDL languages based on Python.
* It's also being used as a verification language.

---
<!-- ###################################################################### -->
## Simulation
<!-- .slide: data-background="#581845" -->
<!-- ###################################################################### -->

[⌂](#/1)

---

### VHDL simulator

|   |   |
|---|---|
| ![GHDL](images/logos/ghdl.png) | Analyzer, compiler, simulator and (experimental) synthesizer for VHDL |
|   |   |

* Full support for IEEE 1076 standard 1987, 1993, 2002 and partial for 2008.
* It can generate executable binary models of the VHDL design, for (co-)simulation.
* It can dump waveforms to multiple formats: VCD, FST or GHW (recommended for VHDL).

---

### Verilog simulators

|   |   |
|---|---|
| ![iVerilog](images/logos/iverilog.png) | IEEE-1364 simulator</br>It generates an intermediate file format wich is then interpreted |
|   |   |

|   |   |
|---|---|
| Verilog/SystemVerilog simulator</br>Compiles into multithreaded C++</br>Performs lint code-quality checks | ![Verilator](images/logos/verilator.png) |
|   |   |

---

### Waveform viewer

|   |   |
|---|---|
| A fully featured wave viewer which reads</br>LXT, LXT2, VZT, FST, and GHW files as</br>well as standard Verilog VCD/EVCD | ![GTKwave](images/screens/gtkwave.png) |
|   |   |

---
<!-- ###################################################################### -->
## Testing and Verification
<!-- .slide: data-background="#581845" -->
<!-- ###################################################################### -->

[⌂](#/1)

---

### HDL based frameworks/methodologies

* **OSVVM:** Open Source VHDL Verification Methodology
* **UVVM:** Universal VHDL Verification Methodology
* **SVUnit:** unit testing framework for Verilog/SystemVerilog

|   |   |   |
|---|---|---|
| ![OSVVM](images/logos/osvvm.png) | ![UVVM](images/logos/uvvm.png) | ![SVUnit](images/logos/svunit.png) |
|   |   |   |

---

### Python aided framework

|   |   |
|---|---|
| ![VUnit](images/logos/vunit.png) | [vunit.github.io](http://vunit.github.io/) |
|   |   |
* **VUnit:** unit testing framework for VHDL/SystemVerilog.
* A Python build and simulator manager together with VHDL libraries.
* Supported simulators: GHDL, Aldec Riviera-PRO, Aldec Active-HDL, Mentor Questa, Mentor ModelSim, Cadence Incisive, Cadence Xcelium.

---

### Python based testbenches

![cocotb](images/logos/cocotb.png)

* **cocotb:** Coroutine Co-simulation Test Bench.
* A coroutine based cosimulation library for writing VHDL and Verilog testbenches in Python, through VPI/VHPI interfaces.
* Supported simulators: GHDL, iverilog, verilator, Synopsys VCS, Aldec Riviera-PRO, Aldec Active-HDL, Mentor Questa, Mentor ModelSim, Cadence Incisive, Cadence Xcelium, Tachyon DA CVC.

----

#### How does cocotb work?

![cocotb overview](images/diagrams/cocotb_overview.png)

**Source:** https://docs.cocotb.org/en/stable

---

### Open Source Verification Bundle (OSVB)

![OSVB](images/diagrams/OSVB.png)

[umarcor.github.io/osvb](https://umarcor.github.io/osvb/)

---

### Formal verification

Using formal mathematic methods (assumptions and assertions) for proving the correctness of intended algorithms/designs.

* **SymbiYosys (sby):** front-end driver program for Yosys-based formal hardware verification flows.
* Supports Verilog (free), VHDL and SystemVerilog (through verific with a license).

![YosysHQ](images/logos/yosys-hq.png)

----

#### Property Specification Language (PSL)

* GHDL provides VHDL support for Yosys/SymbiYosys for free, through ghdl-yosys-plugin.
* Moreover, PSL is supported.

---

### Verification trends

![Verification trends](images/diagrams/verification-trends.png)

**Source:** [ The 2020 Wilson Research Group Functional Verification Study](https://blogs.sw.siemens.com/verificationhorizons/2020/12/16/part-6-the-2020-wilson-research-group-functional-verification-study/) - SIEMENS

See also [GitHub Facts About the HDL Industry](https://larsasplund.github.io/github-facts/)

---
<!-- ###################################################################### -->
## Implementation
<!-- .slide: data-background="#581845" -->
<!-- ###################################################################### -->

[⌂](#/1)

---

### HDL-to-Bitstream

![Implementation](images/diagrams/implementation.png)

**Source:** [hdl/awesome#98](https://github.com/hdl/awesome/issues/98)

---

### Languages

|   |   |
|---|---|
| ![Python](images/logos/python.png) | * nMigen</br>* migen</br> * MyHDL                       |
| ![Scala](images/logos/scala.png)   | * SpinalHDL</br>* Chisel                                |
| Others                             | * Bluespec</br>* Silice</br> * Synthesijer</br> * Clash |
|   |   |

---

### Synthesis

Converting an abstract specification of a circuit (being an HDL a common input) into a design implementation in terms of the basic blocks supported by the chosen technology (being a netlist the output).

----

#### Yosys

* A FOSS framework for RTL synthesis tools.
* It currently has extensive Verilog-2005 support and provides a basic set of synthesis algorithms for various application domains.
* It was the first usable FOSS synthesizer targeting commercially available devices.
* Supports devices from Lattice (iCE40 and ECP5), Xilinx (Series 7, Ultrascale, and others), Gowin, Achronix, Intel, Microsemi, etc.

![Yosys](images/logos/yosys.png)

----

#### GHDL

* Analyzer, compiler, simulator and (experimental) synthesizer for VHDL
* Generates a generic (technology independent) synthesized VHDL (and recently, also Verilog)

* **ghdl-yosys-plugin:** VHDL synthesis, based on GHDL and Yosys.

![GHDL](images/logos/ghdl.png)

---

### Place & Route

|   |   |
|---|---|
| ![NextPnR](images/screens/nextpnr.png) | The stage where the logic elements are placed and interconnected on the FPGA |
|   |   |

* NextPnR (Arachne-pnr)
* VPR, part of Verilog-to-Routing (VTR)

---

### Bitstream Generation

|   |   |
|---|---|
| Packing the result</br>of the P&R into an</br>FPGA configuration</br>file | ![Bitstream](images/diagrams/bitstream.png) |
|   |   |

<!--http://www.fabienm.eu/flf/materiel/liberation-des-fpga/-->

---

### Programming

* **OpenOCD:** **Open** **O**n-**C**hip **D**ebugging, In-System Programming and Boundary-Scan Testing
* **UrJTAG:** universal JTAG library, server and tools
* **iceprog:** programmer of the IceStorm project (FTDI-based programmers)
* **ecpprog:** programmer for the Lattice ECP5 series  (FTDI-based programmers)
* **openFPGALoader:** universal utility for programming FPGA
* **dfu-util:** **D**evice **F**irmware **U**pgrade **Uti**lities (USB)

---
<!-- ###################################################################### -->
## Others
<!-- .slide: data-background="#581845" -->
<!-- ###################################################################### -->

[⌂](#/1)

---

### Project Managers

* **HDLmake:** tool for generating multi-purpose Makefiles for FPGA projects
* **edalize:** a Python Library for interacting with EDA tools (was part of FuseSoC, now its build backend).
* **PyFPGA:** A Python package to use FPGA development tools programmatically

|   |   |   |   |
|---|---|---|---|
| ![PyFPGA](images/logos/pyfpga.png) | Synthesis</br>Implementation</br>Bitstream</br>Programming | ISE, Vivado</br>Quartus</br>Libero-SoC</br>FOSS | **Helpers**</br>hdl2bit</br>prj2bit</br>bitprog |
|   |   |   |   |

---

### Libraries, Collections, IP Cores

* **PoC (Pile of Cores Library):** a library of free, open-source and platform independent IP cores.
* **FuseSoC:** package manager and build abstraction tool (edalize) for FPGA/ASIC development.
* **Litex:** a Migen/MiSoC based SoC builder to easily create Cores/SoCs
* **OpenCores** and **LibreCores:** collections of IPs.
* Several FOSS projects at GitHub and GitLab.

![LiteX](images/logos/litex.png)&nbsp;&nbsp;&nbsp;&nbsp;![OpenCores](images/logos/opencores.png)&nbsp;&nbsp;&nbsp;&nbsp;![LibreCores](images/logos/librecores.png)

---

### Softcores

----

#### Legacy

**Leon 3** (Gaisler)
* 32-bit VHDL processor compliant with the SPARC V8 architecture
* GNU GPL license for research and education
* Part of the GRLIB

**OpenRISC**
* Specification OpenRISC 1000 (32/64 bits)
* The flagship implementation, the OR1200, is written in Verilog
* Part of OpenRISC Reference Platform System-on-Chip (ORPSoC)

----

#### RISC V

![RISC-V](images/diagrams/risc-v.png)

---

### Miscellaneous

----

#### TerosHDL

|   |   |
|---|---|
| ![TerosHDL](images/screens/teroshdl.png) | Atom & VS code</br></br>Suports:</br>GHDL, VUnit & GTKwave</br></br>Coming soon:</br>Verilator, cocotb, edalize |
|   |   |

----

#### Icestudio

![Icestudio](images/screens/icestudio.png)

[FPGAwars/icestudio](https://github.com/FPGAwars/icestudio)

[juanmard/icestudio](https://github.com/juanmard/icestudio) ([nightly](https://github.com/juanmard/icestudio/releases/tag/nightly) builds)

---
<!-- ###################################################################### -->
## Open Hardware
<!-- .slide: data-background="#581845" -->
<!-- ###################################################################### -->

[⌂](#/1)

---

### Kicad

![Kicad](images/screens/kicad.png)

---

### Some ICE40 based boards

|   |   |   |
|---|---|---|
| Fomu</br>![Fomu](images/boards/fomu.png) | iCEBreaker</br>![iCEBreaker](images/boards/icebreaker.png) | iCESugar</br>![iCESugar](images/boards/icesugar.png) |

|   |   |
|---|---|
| TinyFPGA BX</br>![TinyFPGA BX](images/boards/tinyfpga-bx.png) | EDU CIAA FPGA</br>![EDU-CIAA-FPGA](images/boards/edu-ciaa-fpga.png) |

---

### Some ECP5 based boards

|   |   |   |
|---|---|---|
| ULX3S</br>![ULX3S](images/boards/ulx3s.png) |OrangeCrab</br>![OrangeCrab](images/boards/orangecrab.png) | TinyFPGA EX</br>![TinyFPGA EX](images/boards/tinyfpga-ex.png) |
|   |   |   |

---

### Some EOS S3 based boards

|   |   |
|---|---|
| Qomu</br>![Qomu](images/boards/qomu.png) | Quickfeather</br>![QuickFeather](images/boards/quickfeather.png) |
|   |   |

---

### HDL/constraints

* [hdl/constraints](https://github.com/hdl/constraints): constraint files for Hardware Description Language (HDL) designs targeting FPGA boards.
* [hdl.github.io/awesome/boards](https://hdl.github.io/awesome/boards/): list of FPGA developments boards.

---
<!-- ###################################################################### -->
## Final words
<!-- .slide: data-background="#581845" -->
<!-- ###################################################################### -->

[⌂](#/1)

---

### How to be updated?

----

#### Projects - Organizations

![HDL](images/logos/HDL.png)&nbsp;&nbsp;&nbsp;&nbsp;![SymbiFlow](images/logos/symbiflow.png)

![GHDL](images/logos/ghdl.png)&nbsp;&nbsp;&nbsp;&nbsp;![IEEE-P1076.gitlab.io](images/logos/VASG.png)

![FOSSi](images/logos/fossi.png)&nbsp;&nbsp;&nbsp;&nbsp;![OSFPGA](images/logos/osfpga.png)

----

#### People

|   |   |   |
|---|---|---|
| ![GitHub icon](images/icons/github.png)   |  [mithro](https://github.com/mithro) | Tim 'mithro' Ansell                      |
| ![Twitter icon](images/icons/twitter.png) | [mithro](https://twitter.com/mithro) | ![Symbiflow](images/logos/symbiflow.png) |
| ![GitHub icon](images/icons/github.png)   | [umarcor](https://github.com/umarcor)        | Unai Martinez-Corral                 |
| ![Twitter icon](images/icons/twitter.png) | [unaimarcor](https://twitter.com/unaimarcor) | ![umarcor](images/logos/umarcor.png) |

----

#### hdl/awesome

|   |   |
|---|---|
| ![HDL awesome](images/screens/hdl-awesome.png) | ![GHDL in HDL awesome](images/screens/hdl-awesome-ghdl.png) |
|   |   |

[hdl.github.io/awesome](https://hdl.github.io/awesome)

---
<!-- ###################################################################### -->
# Questions?
<!-- .slide: data-background="#1F618D" -->
<!-- ###################################################################### -->

|   |   |
|---|---|
| ![GitHub icon](images/icons/github.png) | [rodrigomelo9](https://github.com/rodrigomelo9) |
| ![Twitter icon](images/icons/twitter.png) | [rodrigomelo9ok](https://twitter.com/rodrigomelo9ok) |
| ![LinkedIn icon](images/icons/linkedin.png) | [rodrigoalejandromelo](https://www.linkedin.com/in/rodrigoalejandromelo/) |
|   |   |
