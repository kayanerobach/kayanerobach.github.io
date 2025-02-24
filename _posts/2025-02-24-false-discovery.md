---
layout: post
title: False Discovery estimation in Record Linkage
date: 2025-02-22 21:37:00
description: A method for estimating the FDR in RL
tags: RecordLinkage, FalseDiscoveryRate
categories: sample-posts
thumbnail: assets/img/FDRAlgo.png
tikzjax: true
---

### Overview

This era of data enables combining information to broaden research opportunities without the expense of new data collection. However, since data are collected for administrative or operational purposes rather than with specific future research questions in mind and, due to privacy reasons, no unique identifier is available. Thus, to assemble observations referring to the same entities,

Record Linkage (RL) algorithms have been developed. RL is a complex task due to the sub-par reliability of the partially identifying variables used to link records and their limited number of unique values. Estimating the False Discovery Rate (FDR) associated with RL therefore holds importance for later inference. In particular in healthcare studies, estimating the Type I error of a set of linked records is crucial to determine the reliability of the inference drawn from the linked data.

We introduce a new method to estimate the FDR and give guidelines for applying it on any sort of RL algorithm. Our recipe consists in linking records from real and synthesised data, estimating the FDR with the synthetic set. Our procedure enables identifying a threshold on the posterior linkage probabilities for which the RL process may be reliable. We investigate the performance of this methodology with well known RL algorithms and data sets before applying it to the Netherlands Perinatal Registry to show the importance of the FDR in RL when studying children/mother dynamics in healthcare records.

### Article

In the paper, we develop our methodology and we illustrate its applicability on real data applications. We detail the different choices made to build the algorithm that estimates the False Discovery Rate for the Record Linkage task. We show how the method informs on the reliability of the linked data and how the FDR estimation can be used as a tool for inference on linked data.

<br>
The code, experiments and data sets are available on GitHub.
<br>
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
    {% include repository/repo.liquid username='robachowyk' repository='robachowyk/FDR-experiments' %}
</div>

### Technical details

<div class="exampletest">
<div align=center>
<br>
<div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/FDRAlgoDev.png" class="img-fluid" %}
    </div>
</div>
</div>
