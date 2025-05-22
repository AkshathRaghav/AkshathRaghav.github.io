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

I'm responsible for parts of the software and hardware aspects of the Memory Subsystem integrated into AMP0/AMP1. This involves ensuring optimal scratchpad usage and QoS through  multi-layered-control starting at the PyTorch Dispatcher through a Software-Controlled Scratchpad and into the Systolic Array FUs. 

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