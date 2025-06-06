---
layout: page
title: RAIS 
description: Defining and leveraging reproducibility factors in AI/ML Research 😎
img: assets/img/rais.jpg
importance: 3
category: software
---

This page expands upon the work I did at the [CVES Group](https://yhlu.net/) (Spring '24), building a workflow to evaluate factors affecting **practical** reproducibility in AI/ML Research projects. I was awarded "Outstanding Sophomore in VIP" for this effort. 

You can find the code [here](https://github.com/AkshathRaghav/RAIS). 

---

## Abstract

Machine learning (ML) software has become a crucial component in many systems. This list includes software published as novel improvements to academic standard, helper packages for AI developers, re-engineered models, etc. If the purpose of the software repository is open code for research community reuse, it should be executable on any system that satisfies the necessary hardware requirements. This requires the inclusion of detailed information such as software dependencies, environmental settings, training hyperparameters, data sourcing, among other related details. Unfortunately, a standardized methodology ensuring reproducibility of AI research results is yet to be established. Many developers fail to reproduce their own reported results. Previous studies have shown that merely publishing the source code is not enough for reproducibility. 

> This project aims to identify key factors that either enhance or impair reproducibility. It will also explore the connections between reproducibility, replicability, and popularity. 


{% include figure.liquid loading="eager" path="assets/img/rais/poster.png" title="poster" class="img-fluid rounded z-depth-1" %}

<div class="caption">
    Poster presented at the Spring EXPO Fair!
</div>


## Methodology

To substantiate the claims made in this project, data from over 3000 repositories (from both academic and corporate research organizations) that have shared codebases for community reuse was collected. The findings are summarized in the sections that follow.

{% include figure.liquid loading="eager" path="assets/img/rais/parallel_coordinates_plot.png" title="parallel" class="img-fluid rounded z-depth-1" %}

{% include figure.liquid loading="eager" path="assets/img/rais/bubble.png" title="bubble" class="img-fluid rounded z-depth-1" %}

{% include figure.liquid loading="eager" path="assets/img/rais/stacked.png" title="stacked" class="img-fluid rounded z-depth-1" %}

{% include figure.liquid loading="eager" path="assets/img/rais/doughnut.png" title="doughnut" class="img-fluid rounded z-depth-1" %}

## Proposed Methodology 

Based on my findings from the collected data, I compiled a workflow that can be used to iteratively identify the crucial and miscellenous aspects of a repository, decide upon a label to present to the codebase as a whole with respect to it's level of replicability, and provide a score to reflect how re-useable it *looks* to be. 

* LHS: I focus on evaluating a repository based on it’s structure, documentation, trustability (certificates), and community engagement. These aspects help us understand how straightforward it is for someone to replicate open-source work, and if there is a reputation for the same.
* RHS: I focus on practicality. My goal is to understand if all the data, code, and metrics are present to (literally) reproduce an experiment. I make my decision tree aimed at classifying repositories into ‘types’ of reproducibility (shown in purple), with a final ‘score’ to reflect the presence of all the required factors (shown in blue).

To view the image in full-screen, click [here](https://drive.google.com/file/d/1uJgJ9iTV1ZUtSjR9FtLMXW5eYRsrIoUN/view?usp=sharing). 

{% include figure.liquid loading="eager" path="assets/img/rais/RAIS.png" title="example image" class="img-fluid rounded z-depth-1" %}



