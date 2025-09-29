---
layout: post
title: Causal Record Linkage
date: 2025-08-06 10:25:00
description: Causal Inference on linked data: when and how?
tags: RecordLinkage, CausalInference, Recoverability
categories: sample-posts
thumbnail: assets/img/CRL.png
tikzjax: true
---

### Overview

Linked data sets present a valuable resource for causal inference by granting access to broader sets of variables across wider populations and extended time periods. Through record linkage, researchers can control for confounding and investigate long-term outcomes. However, understanding when and how causal inference can be performed on linked data remains an overlooked problem

In this project we examine how record linkage conflicts with the assumptions required for identifying causal effects. Our investigation reveals that linkage errors result in inconsistencies and alter exchangeability in the causal framework, leading to attenuation and opposite contribution biases in the inference. In attempting to address these biases by being more stringent on the linkage, positivity is curtailed and sampling bias inadvertently emerges.

We demonstrate how to generalise the effect estimated on rigorously linked data and discuss how linkage decisions should be informed accordingly. Importantly, we identify when existing and novel solutions support valid causal inference on linked data and when inference should be treated with caution or even abandoned. We propose strategies to report on the estimated effect uncertainty and we illustrate the challenges raised and the potential solutions using a simulation study and real data from a Study on Women's Health.

### Article

In this project, we explore the impact of data linkage on the conditions necessary for identification of a causal effect. A trade-off arises: between the bias resulting from linkage errors and the bias resulting from the selection process induced by rigour in the linked data. We provide solutions using generalisability methods to estimate the causal effect on atypical records linked through RL.
<br>

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
    {% include repository/repo.liquid username='robachowyk' repository='robachowyk/CausalRL-experiments' %}
</div>
<br>

### Technical details

Causal Inference can only be performed on reliably linked data, otherwise identification cannot be supported. The process by which pairs of records are linked induces a selection of atypical profiles which are not representative of the initial population targeted by causal inference.
<br>

<div class="exampletest">
<div align=center>
<br>
<div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/FlexRL.png" class="img-fluid" %}
    </div>
<script type="text/tikz">
\begin{tikzpicture}
  \node[shape=circle, draw=black, minimum size=1cm] (x) at (0,0) {$\boldsymbol{X}$};
	\node[shape=circle, draw=black, minimum size=1cm] (t) at (-2,-3) {$T$};
	\node[shape=rectangle, draw=black, minimum size=1cm] (s) at (0,-2) {$S$};
	\node[shape=circle, draw=black, minimum size=1cm] (y) at (2,-3) {$Y$};
  \path [-stealth] (x) edge (s);
  \path [-stealth] (x) edge (t);
  \path [-stealth] (x) edge (y);
  \path [-stealth] (t) edge (y);
\end{tikzpicture}
</script>
<i><font color="#0093af">Selection diagram depicting differences between source population contained in the data and reliably linked population obtained with RL. The selection process $S$ is made on the PIVs included in $\boldsymbol{X}$.</font></i>
<br>
<br>
</div>
</div>

<br>
Therefore, in order to estimate a causal effect from linked data, one has to rely on S-recoverability and G-methods. The main issue with Causal Record Linkage concerns positivity, but it can be waived if one is willing to rely on parametric extrapolation via outcome modelling.
