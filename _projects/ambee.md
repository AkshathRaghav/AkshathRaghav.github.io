---
layout: page
title: forest-fire-forecast
description: Deployed a global fire-risk prediction into Ambee's proprietary API (Funded) 🔥
img: assets/img/ambee/ambee_maddy.jpeg
importance: 2
category: research 
images:
  compare: true
  slider: true
---

This page is the culmination of the work I did at [Ambee](https://www.getambee.com/) (Summer '22) as a Data Science Intern. 

* Created a global Forest-Fire Forecasting system (F3) to integrate into Ambee’s proprietary API dashboard, enabling comprehensive risk assessment. 
* Developed modularized components implemented within an end-to-end ML lifecycle, ensuring continous forecast generation complimented by robust data pipelines. Automated satellite raster retrievel scripts and dockerized big data processing jobs from sources like VIIRS, MODIS, GOES, GMAO, GridMet, etc. Wrote custom scripts for scraping data off more than 16 satellites, from fire-risk data and vegetation to topography and global population density. I had to employ land tiling based on different map projections to concatenate a global data-store from 2012-2022. Many of them have been automated into the API data lakes for the company. 
* Co-authored a research paper highlighting our extensive methodologies that uniquely leverage FWI data to classify world-wide geo-locations into appropritate risk levels. Notably, our models consistently achieve accuracies exceeding 90% across pertinent evaluation metrics for the North America Region, and have been validated against advanced weather-forecast-based ensembles.

The code and data (/sources) extracted from are considered proprietary, and hence cannot be shared. Below, I'm extracting images from our [Paper (Jain, **Ravikiran**, et. al.)](https://www.researchgate.net/publication/372769364_Time-Driven_Fire_Risk_Forecasting_Leveraging_Historical_Trends_for_Enhanced_Seasonal_Modeling), which analyzes our results for the North America region. 

---
# 🔥 Time Driven Fire Risk Forecasting 🔥
--- 

## Abstract
> Wildfires pose severe threats across North America, causing extensive damage to lives, ecosystems, and property. To address this, accurate fire prediction and forecast outlooks are crucial for effective mitigation. Agencies like the National Interagency Fire Center (NIFC) and the Canadian Wildland Fire Information System (CWFIS) provide vital fire risk assessments. In this paper, our main goal was to demonstrate the sufficiency of historical fire risk data for accurate forecasting. Two encoding methods, One-Shot and Year-By-Year, used for encoding the seasonal changes of fire weather, were analyzed for their implications in fire risk assessment, revealing contrasting attributes.  The findings guide model design improvements, bolstering wildfire management and protection measures.

## Data Exploration 

> "During the winter  months ... fire activity is concentrated in the SouthWest and South areas. Spring, .. sees fire season expanding to cover the North, Central, and  South West regions. As summer arrives ... wildfire activity becomes prevalent in multiple regions, including the Northwest, South, Southwest, and East areas. Lastly, autumn ... witnesses thefire season primarily concentrated in the Central region. 

> Additionally, California ... is now experiencing a year-round firerisk  (Cart, 2022, para. 3). Presented below are visualizations of the fire climate regions in  North America, depicting their spatial distribution and corresponding fire risk levels." (Pg. 17)

*FRP is not a weather-based calculation. It is solely expressed as the rate of outgoing thermal radiative energy coming from a burning landscape fire, integrated over all emitted wavelengths and over the hemisphere*

{% include figure.liquid path="assets/img/ambee/image2.png" title="example image" class="img-fluid rounded z-depth-1" %}
{% include figure.liquid path="assets/img/ambee/image3.png" title="example image" class="img-fluid rounded z-depth-1" %}
{% include figure.liquid path="assets/img/ambee/image8.png" title="example image" class="img-fluid rounded z-depth-1" %}
{% include figure.liquid path="assets/img/ambee/image9.png" title="example image" class="img-fluid rounded z-depth-1" %}

Below are some plots discussing our FRP distributions across the years. 

<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/ambee/plots/distributions/image18.png" class="img-fluid rounded z-depth-1" %}</swiper-slide>

  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/ambee/plots/distributions/image16.png" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>
<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/ambee/plots/onevsyr/image13.png" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/ambee/plots/onevsyr/image19.png" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>

--- 

## Comparisons Across 2022-2023 (Training until 2021-split)

Here are some comparisons between the real and predicted FRP maps. 

<img-comparison-slider>
  {% include figure.liquid path="assets/img/ambee/2/image_part_001.jpg" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/ambee/2/image_part_002.jpg" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>
<img-comparison-slider>
  {% include figure.liquid path="assets/img/ambee/8/image_part_001.jpg" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/ambee/8/image_part_002.jpg" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>
<img-comparison-slider>
  {% include figure.liquid path="assets/img/ambee/3/image_part_001.jpg" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/ambee/3/image_part_002.jpg" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>
<img-comparison-slider>
  {% include figure.liquid path="assets/img/ambee/6/image_part_001.jpg" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/ambee/6/image_part_002.jpg" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>
<img-comparison-slider>
  {% include figure.liquid path="assets/img/ambee/oct/image_part_001.jpg" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/ambee/oct/image_part_002.jpg" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>

--- 


## Comparisons Against Govt Forecats 

--- 

### [CWFIS](https://cwfis.cfs.nrcan.gc.ca/maps/forecasts)

<div class="row">
      {% include figure.liquid loading="eager" path="assets/img/ambee/canada/image10.png" title="example image" class="img-fluid rounded z-depth-1" %}
      {% include figure.liquid loading="eager" path="assets/img/ambee/canada/image11.png" title="example image" class="img-fluid rounded z-depth-1" %}
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>

<div class="row">
      {% include figure.liquid loading="eager" path="assets/img/ambee/canada/image21.png" title="example image" class="img-fluid rounded z-depth-1" %}
      {% include figure.liquid loading="eager" path="assets/img/ambee/canada/image25.png" title="example image" class="img-fluid rounded z-depth-1" %}
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>

--- 

### [NIFC](https://www.nifc.gov/nicc-files/predictive/outlooks/monthly_seasonal_outlook.pdf)

        {% include figure.liquid loading="eager" path="assets/img/ambee/america/image2.png" title="example image" class="img-fluid rounded z-depth-1" %}
        {% include figure.liquid loading="eager" path="assets/img/ambee/america/image4.png" title="example image" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>

        {% include figure.liquid loading="eager" path="assets/img/ambee/america/image14.png" title="example image" class="img-fluid rounded z-depth-1" %}
        {% include figure.liquid loading="eager" path="assets/img/ambee/america/image23.png" title="example image" class="img-fluid rounded z-depth-1" %}
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>

--- 


## Results 

Accuracy of 100% allows for difference of 1 level in risk-differentiation. 

{% include figure.liquid loading="eager" path="assets/img/ambee/image.png" title="example image" class="img-fluid rounded z-depth-1" %}
{% include figure.liquid loading="eager" path="assets/img/ambee/image22.png" title="example image" class="img-fluid rounded z-depth-1" %}