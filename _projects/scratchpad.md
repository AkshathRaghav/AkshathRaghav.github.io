---
layout: page
title: scratchpad
description: SW-Managed Parameterizable Scratchpad for the Atalla AI Accelerator
img: assets/img/aihardware/scratchpad/poster.jpg
importance: 1
category: computer-architecture 
images:
  compare: true
  slider: true
---

Modern AI Accelerators, like the Atalla [Ax01 core](https://github.com/Purdue-SoCET/atalla/tree/main), depend on exploiting predictable, high-bandwidth data movement between on-chip memory and compute modules. The Machine Learning (ML) workloads that these specialized chips target inherently expose deterministic access patterns – including tiled matrix multiplication, toeplitz-based convolution, tensor transposes and vector operations. The memory primitive in such architectures are arrays, often called vectors, as opposed to the scalar-optimized general-purpose chips. Additionally, these chips implement memory hierarchies that rely on conventional cache designs, accommodating a wide variety of workloads. These mechanisms are defined by tag overheads, unpredictable latencies, and hardware-based prefetchers that are optimized for adapting to different workload characteristics at runtime. 

In order to study alternate designs that exploit the aforementioned data regularity, Atalla Ax01’s “Scratchpad” architecture implements a parameterizable software-controlled memory subsystem that combines (1) a tile-descriptor-based DMA engine (2) SRAM-banking strategies evaluated on different technology nodes, and (3) four multi-stage interconnect topologies that re-arrange vectors on-the-fly. The architecture provides for swizzle-based movement, avoiding bank-conflicts for wide vector-reads and transpose-friendly micro-op scheduling. 

A core component of the explored design space were the interconnect micro-architectures - Benes, Batcher-Banyan, CLOS - simply referred to as crossbars. All designs were synthesized on the MIT-LL 90nm CMOS process node, and optimized for area, power and clock frequency. A Python-based emulator was built to confirm the viability of the design for the targeted behaviour, and simulated against every possible data-access pattern. The micro-architecture was implemented and modelled at a gate-level using SystemVerilog - within the industry-standard QuestaSim - achieving code coverage of 90%+. 

The work accomplished by this team has laid the foundation for a hardware-software co-designed kernel library that will provide optimized implementations of core vector and matrix operations. In parallel, a custom compiler is being developed to lower this code into instruction bundles, enabling parallel execution of µ-ops to use the asynchronous data-movement features of the Scratchpad. The Atalla Ax01 accelerator will feature a 4-wide tainted-VLIW scheduler, split-transaction AXI-bus and dual-channel DDR4 controller to complement the Scratchpad design. 

Code [here](https://github.com/Purdue-SoCET/atalla/tree/main/rtl/modules/memory/scratchpad). Find our official ECE 696 report [here](https://akshathraghav.github.io/assets/pdf/ScratchpadReport.pdf). 

<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0001.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0002.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0003.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0004.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0005.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0006.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0007.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0008.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0009.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0010.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0011.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0012.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0013.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0014.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0015.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0016.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0017.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0018.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0019.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0020.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0021.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0022.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0023.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0024.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0025.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0026.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0027.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0028.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0029.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0030.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/aihardware/scratchpad/scratchpad_presentation_page-0031.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>
