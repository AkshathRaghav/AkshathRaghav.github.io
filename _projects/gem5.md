---
layout: page
title: gem5-o3-projects
description: WIB and Victim Cache in Gem5's Out-Of-Order x86 CPU
img: assets/img/aihardware/gem5/gem5_img.gif
importance: 3
category: computer-architecture 
---

Instruction window size and cache miss behavior are critical bottlenecks in out-of-order processors. Large instruction windows improve latency tolerance but lengthen critical paths, while conventional cache hierarchies suffer from avoidable conflict misses under memory pressure. This project explores two complementary microarchitectural mechanisms: a Waiting Instruction Buffer (WIB) to decouple load-miss-dependent instruction chains from the issue queue, and a Victim Cache to reduce conflict misses without increasing L1 associativity.

Both mechanisms were implemented and evaluated within the gem5 O3CPU as part of Purdue’s ECE 565 coursework. The work focuses on correctness, integration into gem5’s existing pipeline and cache models, and quantitative evaluation across memory-intensive benchmarks.

## Project1: Waiting Instruction Buffer

Please find the implementation tips [here](). Below, we discuss results.

{% include figure.liquid loading="eager" path="assets/img/gem5/ipc_wib_comparison.png" title="example image" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    IPC Comparison
</div>

We notice that benchmarks with little exposed MLP, or with short load-miss-dependent chains, showcase minimal IPC improvement. This is because not enough wait/ready instructions get transferred into the WIB in order to meaningfully help in instruction flow. For benchmarks that require more pointer-chasing and are memory dependent, the IPC improvement is more noticeable. More instructions are able to get offloaded into the WIB and allow for other future instructions to not get stalled in the front-end.

However, the speedup plateaus as the WIB size increases. The paper also notes that as the WIB size nears the ROB size, the difference is minimal. This is because to exploit the parallelism (and fill the window), more registers (for renaming) and ROB slots (for state) are needed. This leads to stalling the front-end if the WIB is saturated. 

An interesting note from this implementation is that the WIB is often full (for less missRatio-heavy benchmarks), and some instructions stay behind in the IQ because their source registers do not meet the criteria to move to the WIB. As such, when a load miss returns, many dependent instructions are directly considered for issue, instead of having to move out of the WIB first.


## Project2: Victim Cache

Please find the implementation tips [here](). Below, we discuss results.


<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
  <swiper-slide>{% include figure.liquid path="assets/img/gem5/ipc_no_64.png" title="example image" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid path="assets/img/gem5/ipc_64.png" title="example image" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>
<div class="caption">
    IPC Comparison 
</div>


<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
  <swiper-slide>{% include figure.liquid path="assets/img/gem5/missrate_no_64.png" title="example image" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid path="assets/img/gem5/missrate_64.png" title="example image" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>
<div class="caption">
    Miss Rate Comparison
</div>

Since all the benchmarks utilized have memory accesses, the inclusion of the victim cache would always result in a lower miss rate; a victim cache + L1 could be viewed as just an L1 with more size. But the difference in miss rate does correspond to whether or not there is an IPC gain. However, the IPC gain does not always translate. Minimal miss rate difference would lead to a negative IPC gain since the victim cache adds more latency cycles than the benefit gained from a lower miss rate. Benchmarks with a larger miss rate difference, access patterns that exploit more temporal locality, and a higher percentage of memory accesses would demonstrate positive IPC gain. 

The mostly exclusive victim cache often performs better than the no-allocate victim cache. The miss rate for no-allocate is lower for exchange2 and mcf and the same for the others, but only in exchange2 is there a positive IPC gain for it. The likely explanation is that the no-allocate configuration utilizes the victim cache more since clean victim blocks get written to it in addition to dirty, incurring more cycle latency. Thus, no-allocate can only perform better if the percentage difference in miss rate is large enough to overcome the added cycle delays due to writing back more victim blocks. For example, the percentage difference in miss rate for exchange2 is 5% whereas mcf has a difference 0.04%, demonstrating why only exchange2 has a positive IPC gain.