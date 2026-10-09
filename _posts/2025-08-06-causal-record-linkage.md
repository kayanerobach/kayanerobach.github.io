---
layout: post
title: Causal Record Linkage
date: 2025-08-06 10:25:00
description: Causal Inference on linked data when? and how?
tags: RecordLinkage, CausalInference, Recoverability
categories: sample-posts
thumbnail: assets/img/CRL.png
tikzjax: true
---

### Overview

Linked data sets present a valuable resource for causal inference by granting access to broader sets of variables across wider populations and extended time periods. Through record linkage, researchers can control for confounding and investigate long-term outcomes. However, understanding when and how causal inference can be performed on linked data remains an overlooked problem

In this project we examine how record linkage conflicts with the assumptions required for identifying causal effects. Our investigation reveals that linkage errors result in inconsistencies in the causal framework, leading to attenuation bias (due to linked profiles discrepancy and opposite contributions) in the inference. In attempting to address this bias by being more stringent on the linkage, positivity / population distributions overlap are curtailed and sampling bias inadvertently emerges.

We demonstrate how to generalise the effect estimated on rigorously linked data and discuss how linkage decisions should be informed accordingly. Importantly, we identify when existing and novel solutions support valid causal inference on linked data and when inference should be treated with caution or even abandoned. We propose strategies to report on the estimated effect uncertainty and we illustrate the challenges raised and the potential solutions using a simulation study and real data from a Study on Women's Health.

### Article

In this project, we formalise the task of causal inference on linked data, we explore the impact of record linkage on the conditions necessary for identification of a causal effect, we address recoverability from selection sampling bias. A trade-off arises: between the bias resulting from linkage errors and the bias resulting from the selection process induced by rigour in the linked data. We provide solutions using generalisability methods to estimate the causal effect on atypical records linked through record linkage.
<br>

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
    {% include repository/repo.liquid username='robachowyk' repository='robachowyk/CausalRL-experiments' %}
</div>
<br>

### Poster

<div class="row">
<div align=center>
<div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/poster_causal-record-linkage.png" class="img-fluid" %}
    </div>
</div>
</div>

### Technical details

Causal Inference can only be performed on reliably linked data, otherwise identification cannot be supported. The process by which pairs of records are linked induces a selection of atypical profiles which are not representative of the initial population targeted by causal inference.
<br>

<div class="exampletest">
<div align=center>
<div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/selectiondiagram.png" class="img-fluid" %}
    </div>
</div>
</div>

<div class="caption">
    Selection diagrams depicting differences between source population contained in the data and linked population obtained with record linkage (indicated by S). The selection process is made on the linking variables Z overlapping with covariates X, hence S descends from X.
</div>
