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

* Leading on-chip Memory Subsystem for Atalla Tensor Core; focusing on architecture diagramming & ISA design.
* Built a cycle-accurate simulator of the datapath for performance modelling using implicit-convolution and GEMM kernels.
* Architected a parameterizable 2MB Scratchpad with on-the-fly swizzling and a pipelined N × N crossbar – optimized for PPA.
* Designed INT8/FP16 datapaths between Systolic Array & Vector Core; integrating DDR4 controller for asynchronous DRAM transfers.

[Main Repo.](https://github.com/Purdue-SoCET/atalla/tree/main) 

{% include figure.liquid loading="eager" path="assets/img/aihardware/poster.jpeg" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Poster presented to <a href="https://www.linkedin.com/posts/sooraj-chetput_had-a-great-time-presenting-our-ai-hardware-activity-7386455236107923457-dO3a?utm_source=share&utm_medium=member_desktop&rcm=ACoAADOuZO8BODWk4jW2vzRR5RkkFkgH3DoNecE">Semiconductor Leadership Board @ Purdue</a>!
</div>


# scratchpad 

Code [here](https://github.com/Purdue-SoCET/atalla/tree/main/rtl/modules/memory/scratchpad).

{% include figure.liquid loading="eager" path="assets/img/aihardware/scpad_v4.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Top-Level of Atalla's 2MB Scratchpad Arch
</div>

# dcache

Code [here](https://github.com/Purdue-SoCET/atalla/tree/main/rtl/modules/memory/caches).

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

Code [here](https://github.com/Purdue-SoCET/atalla/tree/main/rtl/modules/common/xbar).

{% include figure.liquid loading="eager" path="assets/img/aihardware/crossbar.png" title="poster" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Top-Level of the Full-Mesh and Butterfly Crossbars 
</div>

