---
layout: page
title: accelerated-matrix-processor
description: HW-SW Co-Designed Stack for a custom Tensor-Core (targeting TSMC 70nm)
img: assets/img/aihardware/logo.png
importance: 1
category: microarch 
toc:
  sidebar: left
---

* Leading memory-subsystem development in the AI Hardware team. Responsible for micro-architecture and ISA design.
* Designed \& functionally verified the the lockup-free D-Cache and Systolic Array Controllers integrated into the AMP1 Tensor Core. Synthesized using Cadence Flowtool to 700MHz, and ensured toggle coverage using Siemens QuestaSim.
* Enhanced the AFTx07 RISCV core with the Zicond Ext. for macro-fusion of conditional logic/arithmetic sequences.
* Helped develop semiconductor-design-specific curriculum under the CASCADE Apprenticeship Program w/ Synopsys. 
% * Responsible for ensuring team documentation adherence to standards and assisting with logistics for 200+ students.


{% include figure.liquid loading="eager" path="assets/img/aihardware/logo.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Top-level view of AMP1
</div>

# dcache

{% include figure.liquid loading="eager" path="assets/img/aihardware/dcache_top.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Top-Level of the 4-Way Non-Blocking Parameterizble D-Cache using PLRU replacement. 
</div>

{% include figure.liquid loading="eager" path="assets/img/aihardware/addressing.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Addressing scheme inside each Bank 
</div>

{% include figure.liquid loading="eager" path="assets/img/aihardware/bank.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Inside view of each Bank
</div>

{% include figure.liquid loading="eager" path="assets/img/aihardware/buffer.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Inside view of the MSHR Buffer
</div>

{% include figure.liquid loading="eager" path="assets/img/aihardware/config.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Showcasing Parameters 
</div>



# crossbar 

{% include figure.liquid loading="eager" path="assets/img/aihardware/crossbar.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Top-Level of the Full-Mesh and Butterfly Crossbars 
</div>

# scratchpad + tca 

{% include figure.liquid loading="eager" path="assets/img/aihardware/new_tma.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Top-Level of AMP1's Scratchpad and Compute Accelerator 
</div>