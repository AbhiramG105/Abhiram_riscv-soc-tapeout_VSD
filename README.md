# Abhiram_riscv-soc-tapeout_VSD
# 🖥️ RISC-V Reference SoC Tapeout Program – VSD

[![RISC-V](https://img.shields.io/static/v1?label=RISC-V&message=Open%20ISA&color=%23FF671F&labelColor=%23FF671F&style=for-the-badge)](https://riscv.org/)
[![VSD](https://img.shields.io/static/v1?label=VSD&message=VLSI%20System%20Design&color=FFFFFF&labelColor=FFFFFF&style=for-the-badge&borderColor=000000&borderStyle=solid)](https://www.vlsisystemdesign.com/)
[![ISM](https://img.shields.io/static/v1?label=ISM&message=Make%20in%20India&color=%23046A38&labelColor=%23046A38&style=for-the-badge)](https://www.makeinindia.com/)

Welcome to my repository for the **RISC-V SoC Tapeout Program** organized by **VLSI System Design (VSD)**.  
Here, I’ll be documenting my progress throughout the program in a week-by-week format, with each section capturing the tasks, solutions, and key learnings along the way. This repo is meant to serve as a **personal logbook and reference point**, showing how the journey unfolds from setup to final outcomes.  

---

## 🚀 Program Overview  
In this program, we learn to design a **System-on-Chip (SoC)** from **basic RTL to GDSII** using open-source tools.  
This initiative is part of **India’s largest collaborative RISC-V tapeout program**, empowering **3500+ participants** to build silicon and contribute to the nation’s semiconductor ecosystem.  

---

## 📂 Repository Structure  
The repository is organized on a **week-wise basis**.  
Each week will contain:  
- **Tasks** → Officially assigned weekly objectives  
- **Solutions/Implementations** → Code, design files, or experiments  
- **Documentation** → Notes, explanations, and observations  

This main README serves as the **central dashboard** for navigating the repository.  

```
.
├── README.md
├── Week0/
├── Week1/
├── Week2/
├── Week3/
└── Week4/
```

Note: The above is a visual guide; create folders in the repo to match this layout.

---

## 📅 Weekly Progress  
- [x] [**Week 0**](./Week0/) → Program setup and environment preparation  
- [ ] [**Week 1**](./Week1/) → *(To be updated after official release)*  
- [ ] [**Week 2**](./Week2/) → *(To be updated after official release)*  
- [ ] [**Week 3**](./Week3/) → *(To be updated after official release)*  
- [ ] [**Week 4**](./Week4/) → *(To be updated after official release)*  
- [ ] … *(continues until the final week as per official schedule)*  

---

## 🧰 Toolchain (RTL → GDSII)

| Stage | Tool | Purpose |
| :-- | :-- | :-- |
| RTL Synthesis | [Yosys](https://yosyshq.net/yosys/) | Logic synthesis and technology mapping from Verilog/SystemVerilog (via UHDM) to a gate-level netlist using Liberty timing libraries. |
| Floorplanning | [OpenROAD](https://theopenroadproject.org/) | Die/core sizing, macro placement, power distribution network planning, and initial design constraints. |
| Placement | [OpenROAD](https://theopenroadproject.org/) | Global and detailed placement with timing-driven optimization and congestion management. |
| Clock Tree Synthesis | [OpenROAD](https://theopenroadproject.org/) | Clock network synthesis with buffer/inverter insertion to meet skew and latency targets. |
| Routing | [OpenROAD](https://theopenroadproject.org/) | Global and detailed routing to produce a DRC-clean routed DEF based on PDK rules. |
| Static Timing | [OpenSTA](https://theopenroadproject.org/) | Static Timing Analysis for setup/hold closure using Liberty models and parasitics when available. |
| Physical Verification | [Magic](http://opencircuitdesign.com/magic/) | Design Rule Checking (DRC) and interactive layout edits; antenna and geometry rule checks. |
| LVS | [Netgen](http://opencircuitdesign.com/netgen/) | Layout-vs-Schematic comparison between the extracted layout netlist and the synthesized netlist. |
| Parasitic Extraction | [OpenROAD (SPEF/RCX)](https://theopenroadproject.org/) | RC parasitic extraction to generate SPEF for timing correlation and signoff refinement. |
| GDS Export & View | [KLayout](https://www.klayout.de/) | Final GDSII visualization, layer map inspection, and sanity checks before tapeout packaging. |
| Flow Orchestration | [OpenLane](https://theopenroadproject.org/openlane/) | Automated, reproducible RTL-to-GDSII pipeline coordinating the above tools via configurable stages. |

---

## 🧭 Navigation  
- Start at **Weekly Progress** for high-level tracking.  
- Enter each **Week** folder for tasks, scripts, and results.  
- Use **Issues** for blockers, bug reports, or planning.  
- **Discussions** can host design notes and Q&A.  

Quick links:  
[Week 0](./Week0/) • [Week 1](./Week1/) • [Week 2](./Week2/) • [Week 3](./Week3/) • [Week 4](./Week4/)  
[Issues](../../issues) • [Pull Requests](../../pulls) • [Actions](../../actions)

---

## 📝 Notes  
- Content will be updated **only as per official announcements**.  
- Each week’s folder will be **self-contained** with its own README (if needed).  
- This README remains the **primary index** for the entire repository.  
```
