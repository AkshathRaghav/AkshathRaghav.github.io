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
---

I'm a second-year undergraduate @ Purdue, pursuing a B.Sc in CompE.

My primary interest revolves arould building robust user-facing solutions at the intersection of applied AI, explainable learning paradigms and interoperable systems. I enjoy research-driven environments aimed at taking concepts to tangible products. 

<b>Automatability</b>, <b>reproducibility</b> and <b>accessability</b> remain the core of my work. 

I'm currently looking to get involved in the following: 
- *Vision Generation Algorithms*, 
- *Robot-Environment Interactions*, 
- *GPU Programming*, 
- *Digital Design ↔️ ML/DL*. 

I'd highly appreciate any mentorship or suggestions for research labs @ Purdue that focus on these topics!

## background 

```echarts 
import * as echarts from 'echarts';

var ROOT_PATH = 'https://echarts.apache.org/examples';

var chartDom = document.getElementById('main');
var myChart = echarts.init(chartDom);
var option;

myChart.showLoading();
$.getJSON(ROOT_PATH + '/data/asset/data/les-miserables.json', function (graph) {
  myChart.hideLoading();
  graph.nodes.forEach(function (node) {
    node.label = {
      show: node.symbolSize > 30
    };
  });
  option = {
    title: {
      text: 'Les Miserables',
      subtext: 'Default layout',
      top: 'bottom',
      left: 'right'
    },
    tooltip: {},
    legend: [
      {
        // selectedMode: 'single',
        data: graph.categories.map(function (a) {
          return a.name;
        })
      }
    ],
    animationDuration: 1500,
    animationEasingUpdate: 'quinticInOut',
    series: [
      {
        name: 'Les Miserables',
        type: 'graph',
        layout: 'none',
        data: graph.nodes,
        links: graph.links,
        categories: graph.categories,
        roam: true,
        label: {
          position: 'right',
          formatter: '{b}'
        },
        lineStyle: {
          color: 'source',
          curveness: 0.3
        },
        emphasis: {
          focus: 'adjacency',
          lineStyle: {
            width: 10
          }
        }
      }
    ]
  };
  myChart.setOption(option);
});

option && myChart.setOption(option);
```

* Currently, I'm (almost done) working at the [Duality Lab](https://davisjam.github.io/), where [we're re-engineering](https://akshathraghav.github.io/projects/maskformer/) the MaskFormer segmentation from the [PyTorch-based artifact](https://github.com/facebookresearch/MaskFormer) to TensorFlow for publishing to the TF Model Garden. 
* I'm also involved in MultiModal (LM) understanding projects at the [e-lab](https://e-lab.github.io/); built {[eugenie](https://akshathraghav.github.io/projects/eugenie/), [grammarflow](https://github.com/e-lab/SyntaxShaper/tree/main)} and am working on a (purely research [idea](https://drive.google.com/file/d/1x1IE_1NT-UAO7bFtoc_bPNJgqQFA1AXK/view?usp=sharing)) self-learning document-reading system. 
* Along with this, I led a project at the [CVES](https://yhlu.net/research.html) group, where our goal was to define and evaluate reproducibility within AI/ML projects; wrote the [codebase](https://github.com/AkshathRaghav/RAIS) for data-scraping and [defined](https://akshathraghav.github.io/projects/rais/) evaluation parameters with the same. 
* Previously, I briefly worked on making improvements to the AWS OpenSearch marcobenchmarking project -- proposed PRs for throughput efficiency. 
* I spent the Summer of '23 at [Ambee](https://www.getambee.com/), where I deployed a worldwide [fire forecasting system](https://akshathraghav.github.io/projects/ambee/) into their API and wrote automated scripts for their environment-data focused data lakes. 
* Around the same time, I helped lead a project that was supervised by Prof. Yuan Wang (currently at Stanford) where we aimed to correlate [lightning activity with wildfire spread](https://akshathraghav.github.io/projects/lwl/); I wrote (big-)data-interfacing code for satellites across EUR/EUS/SAR, and packing them dimensionally to use within a ConvLSTM model from [DeepCube's short-term forecasting](https://github.com/DeepCube-org/uc3-public-notebooks/blob/main/3_UC3_DL_models_XAI.ipynb).

## interests

I'm super excited about the [Partner as a Product (PaaP)](https://uxdesign.cc/this-is-the-moment-to-reinvent-your-product-1ee084e38ab1) era we're entering into. I aim to gain experience across the systems we're (going to) base our lives on, from hardware-level programming to cloud-based HA lifecycles. Majoring in ECE gives me the oppurtunity to develop myself in these areas. 

<!-- I aim to specialize in the art of solution-building. My ambition is to bridge cutting-edge research with dynamic market needs, creating useful products robust to customer trends. For now, I'm trying to do so through research, where I have the chance to dive deep and then swim across with applicability, now that I know the depth. I get to build strong fundamentals while keeping my work rooted in practicality.  -->

Lessons from my experiences: 
- *Reliable software is a by-product of a robust design process;*
- *Quality work is replicable, replicable work guarantees quality;*
- *If it's not use(d)(ful), what's the point of building it?*
- *Every unexplained idea in one field finds its explanation within another;*

