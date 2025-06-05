---
layout: page
title: boilernet
description: Compute-Enabled Mini-NAS for Senior Design
img: assets/img/boilernet/Slide6.jpg
importance: 1
category: hardware 
---

<div align="center">
<iframe width="600" height="450" src="https://www.youtube.com/embed/jUlh9KClEwE" title="BoilerNet Overview + Demo -  Senior Design Award - ECE 49022 Spring &#39;25 - Purdue" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

<div style="display: flex; justify-content: center; align-items: center; gap: 1rem;">
  <img src="/assets/img/boilernet/logo.png" alt="logo" style="width: 40%;" />
  <img src="/assets/img/boilernet/boilerNAS_people.jpeg" alt="people" style="width: 50%;" />
</div>

<div class="caption" align="center">
    BoilerNet Team 20! 
    From L to R: Gokulkrishnan Harikrishnan, Akshath Raghav Ravikiran, Aneesh Reddy Poddutur, Gautum Kottayil Nambiar
</div>

## Overview 

This project aimed to develop a Network Attached Storage utilizing ESP32 MCUs. The aptly-named BoilerNet aims to enable In-Network-compute alongside swappable disks and compute workloads, neatly brought together by a cloud-hosted Dashboard interface. There are a few core ideas that form the foundation for this ”cluster” – Low Power Usage, Plug-and-Play Workloads, High Scalability. 

> BoilerNet won the "Senior Design Award" for Spring '25 through Purdue ECE.


{% include theorem.md 
  type="remark"
  name="Disclaimer"
  statement="
    Our reports/presentations are linked in the [/docs](https://github.com/AkshathRaghav/boilernet/tree/main/docs/). They contain in-depth views, reasonings and explanations regarding the design and its motivation. We also outline how we tested and ensured functionality. This repository is just meant to help anyone who wishes to 'refer' to our code/designs for their own use-case. 
  "
%}


<div style="display: flex; justify-content: center; align-items: center; gap: 1rem;">
  <img src="/assets/img/boilernet/top_level.png" alt="logo" style="width: 60%;" />
  <img src="/assets/img/boilernet/top_level_system.png" alt="people" style="width: 30%;" />
</div>
<div class="caption" align="center">
    Top Level System Diagrams
</div>


## Mechanical Design

The physical enclosure consists of six piece types, along with an optional divider: 1x Enclosure Lid, 1x Enclosure Base, 8x compute Enclosures, 8x compute Enclosure Lids, 6x
3mm diameter - 20mm screws, 4x 3mm diameter - 5 mm screws. You can find the related CAD files at [/cad/](https://github.com/AkshathRaghav/boilernet/tree/main/cad/) w/o dependencies. Reach out to [Aneesh Poddutur](https://www.linkedin.com/in/aneesh-poddutur/) for more information. 


{% include figure.liquid loading="eager" path="/assets/img/boilernet/mechanical_first.png" title="poster" class="img-fluid rounded z-depth-1" %}

<div class="caption" align="center">
    Physical Enclosure
</div>


{% include figure.liquid loading="eager" path="/assets/img/boilernet/second.drawio.png" title="poster" class="img-fluid rounded z-depth-1" %}

<div class="caption" align="center">
    Top Enclosure
</div>



{% include figure.liquid loading="eager" path="/assets/img/boilernet/mechanical_third.png" title="poster" class="img-fluid rounded z-depth-1" %}

<div class="caption" align="center">
    Compute Enclosure
</div>

<div align="center">
  <img src= alt="third" style="height: 50%;"/>
</div>

{% include figure.liquid loading="eager" path="/assets/img/boilernet/Slide6.jpg" title="poster" class="img-fluid rounded z-depth-1" %}

<div class="caption" align="center">
    Assembled System!
</div>

## PCB Design

This was our first time working on PCB Design, and had a few fly-wires hanging about. Below is one of the slides we usd in our [Final Presentation](/docs/Final%20Design%20Review.pdf) to sound endearing ;)

You can find our PCB Designs at [/gerbers/](https://github.com/AkshathRaghav/boilernet/tree/main/gerbers/) and [/kicad_projects](https://github.com/AkshathRaghav/boilernet/tree/main/kicad_projects/)! Reach out to [Gautam Nambiar](https://www.linkedin.com/in/gautam-nambiar-821479251/) and [Gokul Harikrishnan](https://www.linkedin.com/in/gokulkrishnan-harikrishnan-40334b227/) if you have any questions.



{% include figure.liquid loading="eager" path="/assets/img/boilernet/pcb_network.png" title="poster" class="img-fluid rounded z-depth-1" %}

<div class="caption" align="center">
    Network/Switch PCB
</div>


{% include figure.liquid loading="eager" path="/assets/img/boilernet/pcb_compute.png" title="poster" class="img-fluid rounded z-depth-1" %}

<div class="caption" align="center">
    Compute Node PCB
</div>

## Software 

All the code for the MCUs are maintained within the [/src](https://github.com/AkshathRaghav/boilernet/tree/main/src/) folder. Each node's build is maintained within it's own ESP-IDF setup, and can be configured in isolation. 
[/model_train](https://github.com/AkshathRaghav/boilernet/tree/main/model_train/) contains the code for training the models and preparing weights to flashed through [https://github.com/AkshathRaghav/boilernet/tree/main/compute_nodes](https://github.com/AkshathRaghav/boilernet/tree/main/src/compute_nodes/). Please reach out to [Akshath Raghav](https://www.linkedin.com/in/akshathrr/) if you have any questions!

- [/src/fastapi_backend](https://github.com/AkshathRaghav/boilernet/tree/main/src/fastapi_backend/) and [/src/streamlit_frontend](https://github.com/AkshathRaghav/boilernet/tree/main/src/streamlit_frontend/) can be configured using the Makefiles. Try `make venv; make setup; make run`. 
- [/src/network_node](https://github.com/AkshathRaghav/boilernet/tree/main/src/network_node/), [/src/switch_nodes](https://github.com/AkshathRaghav/boilernet/tree/main/src/switch_nodes/) and [/src/compute_nodes](https://github.com/AkshathRaghav/boilernet/tree/main/src/compute_nodes/) require `idf.py` configured and `IDF_PATH` set up. Remember, `idf.py` should be run in an ESP-IDF project directory, i.e., a directory containing a CMakeLists.txt file. `idf.py fullclean; idf.py build; idf.py flash -port /dev/ttyUSB1` will be sufficient. 
- [/model_train/extract.sh](https://github.com/AkshathRaghav/boilernet/tree/main/model_train/extract.sh) has the script for setting up ImageNet -- only if you want to train your own subsets. Thanks to [BIGBALLON](https://gist.github.com/BIGBALLON) for this [script](https://gist.github.com/BIGBALLON/8a71d225eff18d88e469e6ea9b39cef4). 
- [/model_train/train.py](https://github.com/AkshathRaghav/boilernet/tree/main/model_train/train.py) and [/model_train/convert_and_header.py](https://github.com/AkshathRaghav/boilernet/tree/main/model_train/convert_and_header.py) will set you up quickly with training your MobileNet or EfficientNet backbones with a head for the subset you've chosen, and then quantizing them (w/ additional calibration tuning). Results will be put into [/model_train/models](https://github.com/AkshathRaghav/boilernet/tree/main/model_train/models/) and [/model_train/quantized_models](https://github.com/AkshathRaghav/boilernet/tree/main/model_train/quantized_models/). After you're done training, put the chosen header (.cc) file into [/src/compute_nodes/main](https://github.com/AkshathRaghav/boilernet/tree/main/src/compute_nodes/main/) and put this file name into Line 5 in [/src/compute_nodes/main/CMakeLists.txt](/src/compute_nodes/main/CMakeLists.txt). 
