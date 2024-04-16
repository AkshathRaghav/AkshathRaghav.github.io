---
layout: about
title: about
permalink: /
subtitle: ECE @ <a href='https://engineering.purdue.edu/ECE'>Purdue</a> | <a href='araviki@purdue.edu'>araviki@purdue.edu</a>

profile:
  align: right
  image: profile_pic.jpg
  image_circular: true # crops the image to make it circular
  more_info: 
  
news: true # includes a list of news items
latest_posts: true # includes a list of the newest posts
selected_papers: true # includes a list of papers marked as "selected={true}"
social: false # includes social icons at the bottom of the page
mermaid:
  enabled: true
  zoomable: true 
---

I'm a second-year undergraduate @ Purdue, pursuing a B.Sc in CompE.

My primary interest revolves arould building robust user-facing solutions at the intersection of explainable learning algorithms and interoperable systems. I enjoy research-driven environments aimed at taking concepts to tangible products. 

<b>Automatability</b>, <b>reproducibility</b> and <b>accessability</b> remain the core of my work. 

I'm currently looking to get involved in the following: 
- *Vision Generation Algorithms*, 
- *Robot-Environment Interactions*, 
- *GPU Programming*, 
- *Digital Design ↔️ ML/DL*. 

I'd highly appreciate any mentorship or suggestions for research labs @ Purdue that focus on these topics!

## background 

```mermaid
classDiagram
    class SWE_Research{
        << (red) >>
        Duality_Lab
        CVES
    }
    class ML_Research{
        << (red) >>
        Duality_Lab
        Ambee
        LWL
    }
    class AI_Research{
        << (red) >>
        e-lab
    }
    class MLOps{
        << (red) >>
        Linux
        Docker
        DVC
        MLFlow
        Kafka
        Redis
    }
    class Backend{
        << (red) >>
        MongoDB
        PostgreSQL
        OpenSearch
        DynamoDB
    }
    class Duality_Lab{
        << (blue) >>
        TensorFlow
        PyTorch
        TPUs_GPUs
        GCP
        Unit_Differential_Tests
    }
    class Ambee{
        << (blue) >>
        Data_Engineering
        Big_Data
        AWS_Glue
        AWS_Spark
        DevOps
    }
    class e_lab{
        << (blue) >>
        LLMs
        AI_Agents
        NLP
        GPUs
    }
    class LWL{
        << (blue) >>
        Big_Data
        Xarray
        Geospatial_ML
        GIS
        GeoPandas
    }
    class CVES{
        << (blue) >>
        AI_Agents
        DVC
    }

    %% Linking Classes
    SWE_Research -- Duality_Lab
    SWE_Research -- CVES
    ML_Research -- Duality_Lab
    ML_Research -- Ambee
    ML_Research -- LWL
    AI_Research -- e_lab

    %% Coloring Specific Skills under Each Organization
    class TensorFlow{ << (pink) >> }
    class PyTorch{ << (pink) >> }
    class TPUs_GPUs{ << (pink) >> }
    class GCP{ << (pink) >> }
    class Unit_Differential_Tests{ << (pink) >> }
    class Data_Engineering{ << (pink) >> }
    class Big_Data{ << (pink) >> }
    class AWS_Glue{ << (pink) >> }
    class AWS_Spark{ << (pink) >> }
    class DevOps{ << (pink) >> }
    class LLMs{ << (pink) >> }
    class AI_Agents{ << (pink) >> }
    class NLP{ << (pink) >> }
    class GPUs{ << (pink) >> }
    class Xarray{ << (pink) >> }
    class Geospatial_ML{ << (pink) >> }
    class GIS{ << (pink) >> }
    class GeoPandas{ << (pink) >> }
    class DVC{ << (pink) >> }
```

* F'23 - S'24: I worked at the [Duality Lab](https://davisjam.github.io/), where [we re-engineered](https://akshathraghav.github.io/projects/maskformer/) the MaskFormer segmentation from the [PyTorch-based artifact](https://github.com/facebookresearch/MaskFormer) to TensorFlow for publishing to the TF Model Garden. You can find our paper [here]() and code [here](https://github.com/PurdueDualityLab/tf-maskformer/tree/PR_Draft/models/official/projects/maskformer). I also generated figures for the [PeaTMOSS paper](https://arxiv.org/pdf/2402.00699.pdf).
* S'24: I'm involved in MultiModal (LM) understanding projects at the [e-lab](https://e-lab.github.io/). I've built [eugenie](https://akshathraghav.github.io/projects/eugenie/) & [grammarflow](https://github.com/e-lab/SyntaxShaper/tree/main) and am working on encoding reading-order patterns within documents ([here's](https://drive.google.com/file/d/1x1IE_1NT-UAO7bFtoc_bPNJgqQFA1AXK/view?usp=sharing) my current plan of action)
* S'24: I led a project at the [CVES](https://yhlu.net/research.html) group @ Purdue ECE, where our goal was to define and evaluate reproducibility within AI/ML projects. I wrote the [codebase](https://github.com/AkshathRaghav/RAIS) for building our pipeline and statistically [defined](https://akshathraghav.github.io/projects/rais/) the importance of parameters. 
* S'23 - Summer'23: Worked at [Ambee](https://www.getambee.com/), where I deployed a worldwide [fire forecasting system (F3)](https://akshathraghav.github.io/projects/ambee/) into their API and wrote automated scripts for their environment-data focused [data lakes](https://www.getambee.com/api-documentation). You can find my **LOR** [here](https://akshathraghav.github.io/assets/pdf/AkshathRaghavR_LOR_Ambee.pdf). You can find the whitepaper [here](https://www.researchgate.net/publication/372769364_Time-Driven_Fire_Risk_Forecasting_Leveraging_Historical_Trends_for_Enhanced_Seasonal_Modeling). 
* F'22 - S'23: I helped lead a project that was supervised by Prof. [Yuan Wang](https://wang-lab.stanford.edu/people/yuan-wang) (currently at Stanford) where we aimed to correlate [lightning activity with wildfire spread](https://akshathraghav.github.io/projects/lwl/). I wrote (big-)data-interfacing code for satellites across EUR/EUS/SAR, and was responsible for packing them to use within a ConvLSTM model from [DeepCube's short-term forecasting](https://github.com/DeepCube-org/uc3-public-notebooks/blob/main/3_UC3_DL_models_XAI.ipynb).

## interests

I'm super excited about the [Partner as a Product (PaaP)](https://uxdesign.cc/this-is-the-moment-to-reinvent-your-product-1ee084e38ab1) era we're entering into. I hope to gain experience across the systems we're (going to) base our lives on, from hardware-level programming to cloud-based HA lifecycles. Majoring in ECE gives me the oppurtunity to develop myself in these areas. 

Going forward, I aim to specialize in the art of **solution-building**, by bridging happening research with dynamic market needs. My approach involves deep-diving into research to understand core principles thoroughly and then 'swimming' across to explore its applications, ensuring my projects are both **fundamentally robust and practically relevant**.

Lessons from my mentors: 
- *Reliable software is a by-product of a robust design process;*
- *Quality work is replicable, replicable work guarantees quality;*
- *If it's not use(d)(ful), what's the point of building it?*
- *Every unexplained idea in one field finds its explanation within another*

