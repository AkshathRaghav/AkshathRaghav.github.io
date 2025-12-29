---
layout: page
title: wallace-tree-multiplier
description: 8-bit Wallace Tree Multiplier implementation on GPDK45nm
img: assets/img/559/parex.png
importance: 4
category: computer-architecture 
images:
  compare: true
  slider: true
---

Find our official ECE 559 report [here](https://akshathraghav.github.io/assets/pdf/8bitWTM.pdf). 

A Wallace Tree Multiplier (WTM) accelerates integer multiplication by reducing partial-products in parallel using carry-save-adder (CSA) chains, followed by a final ripple-carry-adder (RCA) stage. This project successfully implemented an 8-bit WTM using the inversion property to minimize total area. Post-layout validation using the GPDK45nm process library verified that the design met all core requirements with

* a worst-case delay of 1.742 ns at 1V and 1.3948 ns at 1.1V, and
* an energy consumption of 320.712 fJ at 1V and 395.945 fJ at 1.1V 

for the worst-case delay. The exploitation of the inversion property also reduced the overall transistor count by 298, leaving the final chip area measuring at 3305.51 um^2. Parasitic extraction resulted in near doubling of the worst-case delay and energy consumption results, but the metrics remained well within the specifications, having a positive slack of 

* 0.758 ns & 529.288 fJ at 1V, and 
* 1.1052 ns & 454.055 fJ at 1.1V. 


{% include figure.liquid loading="eager" path="assets/img/559/schem.png" title="example image" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    WTM Schematic
</div>

<img-comparison-slider>
  {% include figure.liquid path="assets/img/559/WTM_Labeled_layout.png" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/559/parex.png" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>
<div class="caption">
    WTM Layout vs Post-Extraction Layout
</div>

{% include figure.liquid loading="eager" path="assets/img/559/PPG_Labeled_layout.png" title="example image" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Partial Product Generation
</div>

{% include figure.liquid loading="eager" path="assets/img/559/wtm_full.png" title="example image" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Reduction Stages Diagram
</div>

<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
  <swiper-slide>{% include figure.liquid path="assets/img/559/Stage1_Labeled_layout.png" title="example image" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid path="assets/img/559/Stage2_Labeled_layout.png" title="example image" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid path="assets/img/559/Stage3_Labeled_layout.png" title="example image" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid path="assets/img/559/Stage4_Labeled_layout.png" title="example image" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>
<div class="caption">
    Reduction Stages Layout 
</div>

{% include figure.liquid loading="eager" path="assets/img/559/testbench.png" title="example image" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    WTM Testbench
</div>

| Voltage (V) | Schematic Delay (ns) | Layout Delay (ns) | Delay Delta (ns) |
|:-----------:|:--------------------:|:-----------------:|:----------------:|
|     1.0     |        0.8164        |       1.742       |     +0.9256      |
|     1.1     |        0.6498        |      1.3948       |     +0.7450      |
{: .table .table-bordered .table-sm }
<div class="caption">
    Worst-Case Delay
</div>

| Voltage (V) | Schematic Energy (fJ) | Layout Energy (fJ) | Energy Delta (fJ) |
|:-----------:|:---------------------:|:------------------:|:-----------------:|
|     1.0     |        363.920        |      741.147       |     +377.227      |
|     1.1     |        450.868        |      907.942       |     +457.074      |
{: .table .table-bordered .table-sm }
<div class="caption">
    Worst-Case Energy
</div>

| Cell Type            | Num. Inst. | Transistors / Inst. | Total Transistors |
|:---------------------|:----------:|:-------------------:|:-----------------:|
| FAInv                |     64     |         24          |       1536        |
| Inverter             |     43     |          2          |         86        |
| NAND                 |     64     |          4          |        256        |
| **Inverted Total**   |     —      |          —          |      **1878**     |
| FA                   |     64     |         28          |       1792        |
| AND                  |     64     |          6          |        384        |
| **Non-Inverted Total** |   —      |          —          |      **2176**     |
{: .table .table-bordered .table-sm }
<div class="caption">
    Transistor Count Breakdown
</div>