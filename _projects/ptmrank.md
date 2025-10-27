---
layout: page
title: ptmrank
description: Precision rank popular PTMs against your use-case ⚒️
img: assets/img/hf.png
importance: 9
category: software
---

## Overview 

PTMRank is meant to help in gauging the transferrability of Pre Trained Deep Neural Networks (/Models) towards a downstream task. This work was inspired by the author's previous contributions to the PeaTMOSS artifact [(PeaTMOSS: A Dataset and Initial Analysis of Pre-Trained Models in Open-Source Software)](https://arxiv.org/abs/2402.00699). 

## Supported Metrics

* **ETran** [[Code]](/ptmrank/metrics/ETran.py)  <= [[ICCV 2023]](https://openaccess.thecvf.com/content/ICCV2023/papers/Gholami_ETran_Energy-Based_Transferability_Estimation_ICCV_2023_paper.pdf)  ETran: Energy-Based Transferability Estimation 
* **PED** [[Code]](/ptmrank/metrics/PED.py)  <= [[ICCV 2023]](https://openaccess.thecvf.com/content/ICCV2023/papers/Li_Exploring_Model_Transferability_through_the_Lens_of_Potential_Energy_ICCV_2023_paper.pdf) Exploring Model Transferability through the Lens of Potential Energy 
* **EMMS** [[Code]](/ptmrank/metrics/EMMS.py)  <= [[NEURIPS 2023]](https://proceedings.neurips.cc/paper_files/paper/2023/file/687b7b2bdcc2ced577c0a989b44e7078-Paper-Conference.pdf) Foundation Model is Efficient Multimodal Multitask Model Selector 
* **GBC** [[Code]](/ptmrank/metrics/GBC.py)  <= [[CVPR 2022]](https://openaccess.thecvf.com/content/CVPR2022/papers/Pandy_Transferability_Estimation_Using_Bhattacharyya_Class_Separability_CVPR_2022_paper.pdf) Transferability Estimation using Bhattacharyya Class Separability
* **SFDA** [[Code]](/ptmrank/metrics/SFDA.py)  <= [[ECCV 2022]](https://www.ecva.net/papers/eccv_2022/papers_ECCV/papers/136940279.pdf) Not All Models Are Equal: Predicting Model Transferability in a Self-challenging Fisher Space
* **TransRate** [[Code]](/ptmrank/metrics/TransRate.py)  <=  [[ICML 2022]](https://proceedings.mlr.press/v162/huang22d/huang22d.pdf) Frustratingly Easy Transferability Estimation
* **PACTran** [[Code]](/ptmrank/metrics/PACTran.py)  <= [[ECCV 2022]](https://arxiv.org/abs/2203.05126) PACTran: PAC-Bayesian Metrics for Estimating the Transferability of Pretrained Models to Classification Tasks
* **NLEEP** [[Code]](/ptmrank/metrics/NLEEP.py)  <= [[CVPR 2021]](https://openaccess.thecvf.com/content/CVPR2021/papers/Li_Ranking_Neural_Checkpoints_CVPR_2021_paper.pdf) Ranking Neural Checkpoints
* **LogME** [[Code]](/ptmrank/metrics/LogME.py)  <= [[ICML 2021]](https://arxiv.org/pdf/2102.11005.pdf) Log Maximum Evidence in `LogME: Practical Assessment of Pre-trained Models for Transfer Learning
* **LEEP** [[Code]](/ptmrank/metrics/LEEP.py)  <= [[ICML 2020]](http://proceedings.mlr.press/v119/nguyen20b/nguyen20b.pdf) LEEP: A New Measure to Evaluate Transferability of Learned Representations 
* **H-Score** [[Code]](/ptmrank/metrics/HScore.py)  <= [[ICIP 2019]](http://yangli-feasibility.com/home/media/icip-19.pdf) An Information-theoretic Approach to Transferability in Task Transfer Learning 
* **NCE** [[Code]](/ptmrank/metrics/NCE.py)  <= [[ICCV 2019]](https://arxiv.org/pdf/1908.08142v1.pdf) Negative Conditional Entropy in `Transferability and Hardness of Supervised Classification Tasks
* **WDJE** [[Code]](/ptmrank/metrics/WDJE.py)  <= [[arXiv]](https://arxiv.org/abs/2305.06741) To transfer or not transfer: Unified transferability metric and analysis 

## Example

```
from ptmrank.benchmarker import Benchmarker
from ptmrank.models import ModelsPeatMOSS, Model, Models
from Examples import (
    load_image_example,
    load_text_example,
    load_audio_example,
)

# models = Models([Model(model_name=<>,ckpt=<>,embedding_function=<>)...])
models = ModelsPeatMOSS('./mapping.json')['image-classification'] # Selects PeaTMOSS PTMs 

# Sets the pipeline for a specific metric
benchmarker = Benchmarker(
    models, store_features='./checkpoints', 
    logme=True, regression=False, auto_increment_if_failed=True
)

# ./ptmrank/examples.py shows porting your files into PTMRank Dataloaders
benchmarker('image-classification', load_image_example(), 5)
```

