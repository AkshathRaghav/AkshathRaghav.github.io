---
layout: page
title: accelerated-matrix-processor
description: HW-SW Co-Designed Stack for a custom Tensor-Core (targeting TSMC 70nm)
img: assets/img/aihardware/logo.png
importance: 1
category: microarch 
related_publications: true
toc:
  sidebar: left
---

I'm responsible for parts of the software and hardware aspects of the Memory Subsystem integrated into AMP0/AMP1. This involves ensuring optimal scratchpad usage and QoS through  multi-layered-control starting at the PyTorch Dispatcher.  

{% include figure.liquid loading="eager" path="assets/img/aihardware/logo.png" title="poster" class="img-fluid rounded z-depth-1" %}

# dcache

{% include figure.liquid loading="eager" path="assets/img/aihardware/dcache_top.png" title="poster" class="img-fluid rounded z-depth-1" %}
{% include figure.liquid loading="eager" path="assets/img/aihardware/addressing.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}
{% include figure.liquid loading="eager" path="assets/img/aihardware/bank.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}
{% include figure.liquid loading="eager" path="assets/img/aihardware/buffer.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}
{% include figure.liquid loading="eager" path="assets/img/aihardware/config.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}


# crossbar 

{% include figure.liquid loading="eager" path="assets/img/aihardware/crossbar.png" title="poster" class="img-fluid rounded z-depth-1" %}


# scratchpad + tca 

{% include figure.liquid loading="eager" path="assets/img/aihardware/new_tma.png" title="poster" class="img-fluid rounded z-depth-1" %}
