---
layout: post
title: False Discovery estimation in Record Linkage
date: 2025-03-26 21:37:00
description: A method for estimating the FDP in RL
tags: RecordLinkage, FalseDiscoveryProportion
categories: sample-posts
thumbnail: assets/img/FDPimg.png
tikzjax: true
---

### Overview

This era of data enables combining information to broaden research opportunities without the expense of new data collection. However, since data are collected for administrative or operational purposes rather than with specific future research questions in mind and, due to privacy reasons, no unique identifier is available. Thus, to assemble observations referring to the same entities, Record Linkage (RL) algorithms have been developed.

RL probabilistically link records based on partially identifying variables. Since these variables lack the strength to perfectly combine information, RL procedures yield an imperfect set of linked records. Estimating the False Discovery Proportion (FDP) associated with RL therefore holds importance for later inference. In particular in healthcare studies, estimating the Type I error of a set of linked records is crucial to determine the reliability of the inference drawn from the linked data.

We introduce a novel method for estimating the FDP in RL for two overlapping data sets. We synthesise data from their estimated empirical distribution and use it along with real data in the linkage process. Since synthetic records cannot form links with real entities, they provide a means to estimate the amount of falsely linked pairs. Notably, this method applies to all RL techniques and across diverse settings where links and non-links have similar distributions, which is typical in complex tasks with poorly discriminative linking variables and multiple records sharing similar information while representing different entities. By identifying the FDP in RL and selecting suitable model parameters, our approach enables to assess and improve the reliability of linked data.

We evaluate the performance of this methodology using established RL algorithms and benchmark data applications before deploying it to link siblings from the Netherlands Perinatal Registry, where the reliability of previous RL applications has never been confirmed. Through this application, we highlight the importance of accounting for linkage errors when studying mother-child dynamics in healthcare records.

### Article

In the paper, we develop our methodology and we illustrate its applicability on real data applications. We detail the different choices made to build the algorithm that estimates the False Discovery Proportion for the Record Linkage task. We show how the method informs on the reliability of the linked data and how the FDP estimation can be used as a tool for inference on linked data.
<br>

<div style="margin-left: 30px;">
  <a href="https://arxiv.org/abs/2503.20627" target="_blank" rel="noopener noreferrer">
    <i class="fa-solid fa-file" title="Arxiv" style="font-size: 74px;"></i>
    <span style="font-size: 24px;">arXiv</span>
  </a> 
</div>

<br>
The code, experiments and data sets are available on GitHub.
<br>
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
    {% include repository/repo.liquid username='robachowyk' repository='robachowyk/FDPinRL-experiments' %}
</div>
<br>

<i>Cite the paper:</i>
<br>
@article{robachetal2025,
<br>
author = {Robach, Kayané and Hof, Michel H and van de Wiel, Mark A},
<br>
title = {False Discovery estimation in Record Linkage},
<br>
journal = {Statistics in Medicine},
<br>
pages = {},
<br>
year = {2025},
<br>
month = {09},
<br>
issn = {},
<br>
doi = {},
<br>
url = {}
<br>
}

### Technical details

<div class="exampletest">
<div align=center>
<div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/FDPalgo.png" class="img-fluid" %}
    </div>
</div>
</div>
