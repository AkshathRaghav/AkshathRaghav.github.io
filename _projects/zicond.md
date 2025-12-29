---
layout: page
title: zicond
description: Zicond Extension implemented in the SoCET RISCV Core 
img: assets/img/zicond.png
importance: 7
category: computer-architecture
---

The Zicond Extension aims to enhance the RISC-V instruction set architecture by introducing a simplistic pair of conditional instructions. Traditional condition-based operations in RISC-V involve using multiple instructions and branches to evaluate and execute actions, leading to increased code complexity and a higher rate of branch mispredictions. This extension addresses this inefficiency by allowing for register-to-register operations that require a smarter, but reliable, use of register values to negate the use of branches. Furthermore, the current RISC-V core being developed for the upcoming AFTx07 chip tape-out does not have a branch predictor implemented, underscoring the necessity of this project.

The primary objective of this project is to implement and verify the functionality of the Zicond extension within the existing RISC-V architecture. This includes designing the new instructions, integrating them into the core, and creating comprehensive testbenches to ensure correct implementation and performance benefits. By addressing the lack of branch prediction in the current core, this project seeks to significantly improve the robustness of the AFTx07 chip.

You can find the code [here](https://github.com/Purdue-SoCET/RISCVBusiness/tree/rv32zc) and my presentation [here](https://www.youtube.com/watch?v=b4FaUyiJN7s).

**For Purdue SoCET Students:** You can find a guide to working with RISCVBusiness/FuseSoC/Verilator to add extensions [here](https://purdue0.sharepoint.com/sites/ENGR-ECE-O-SOCET/_layouts/15/Doc.aspx?sourcedoc={5f14e671-9db9-46fa-9b9a-5daf42d18627}&action=edit&wd=target%28Untitled%20Section.one%7Ce1464c9b-5e1e-4a58-ba0e-5f80be47075a%2FGuide%20Adding%20Extensions%20to%20RISCV-Business%7C38e77aae-7fb6-40ea-aa88-109885970be0%2F%29&wdorigin=NavigationUrl)

