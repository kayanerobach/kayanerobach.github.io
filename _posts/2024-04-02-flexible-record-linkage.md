---
layout: post
title: Flexible Record Linkage
date: 2024-04-02 11:46:00
description: Stochastic Expectation Maximisation for combining information spread over two files
tags: RL LatentModel PIVs StEM
categories: sample-posts
thumbnail: assets/img/FlexRL.png
tikzjax: true
---

Combining data from various sources such as observational studies and municipality registries or hospital databases empowers researchers to explore innovative questions and improve models. However, the lack of a unique identifier often poses challenges. Natural problems like counting casualties require distinguishing individuals in registers that may contain duplicates when bodies are listed by several organisations. Conducting healthcare longitudinal studies require follow up information that is often concealed due to privacy considerations.

Record linkage procedures determine whether pairs of observations collected on different occasions belong to the same individual using partially identifying variables (e.g. initials, birth year, zipcode), herafter denoted PIVs. The complexity of this problem stems from the sub-par reliability of the PIVs used to link records and their limited number of unique values. Furthermore, because everyone is often uniquely represented in each file, records from one file can maximally be linked with one record in the other file, making the linkage decisions interdependent.

We propose a Stochastic Expectation Maximisation to combine observations from two overlapping data sets, that adapts to varying data complexities, addressing registration errors, including inaccuracies and missing values, and accommodating changes of the identifying information over time. Taking account of zip code temporal dynamics holds importance in healthcare longitudinal studies; in the particular case of survival analysis, long term follow-up are crucial, which increases the probability to move.

In the paper, we illustrate the ability of our methodology to connect observations using two large real data applications and demonstrate the robustness of our model to the linking variables quality in a simulation study.

<br>
<div style="margin-left: 30px;">
  <a href="https://info.arxiv.org/help/submit_tex.html" target="_blank" rel="noopener noreferrer">
    <i class="fa-solid fa-file-pdf" style="font-size: 74px;"></i>
  </a>
</div>
<br>

The proposed algorithm FlexRL is available in R. The source code, supplementary materials and data sets are available on GitHub.

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
    {% include repository/repo.liquid username='robachowyk' repository='robachowyk/RecordLinkage/tree/main/FlexRL' %}
</div>

<br>
<br>
<i>More technical details:</i>

To estimate the common set of records, we build a statistical model that leverages the latent representation of the partially identifying information embedded in the data generation process, and derive a probabilistic estimate that allows for inference. We estimate the model parameters represented as input nodes on the probabilistic graphical model hereafter, using a Stochastic Expectation Maximisation algorithm.
<br>

<div class="exampletest">
<div align=center>
<br>
<script type="text/tikz">
\begin{tikzpicture}
\node[draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (gamma) at (0,4) {$\gamma$};
\node[shape=circle, draw={rgb:red,0;green,147;blue,175}, dashed, minimum size=1cm] (delta) at (0,2) {$\Delta$};
\node[draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (eta) at (0,0) {$\eta$};
\node[draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (alpha) at (0,-2) {$\alpha$};
\node[shape=circle, dashed, draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (HA) at (-3,-2) {$H^A$};
\node[shape=circle, dashed, draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (HB) at (3,-2) {$H^B$};
\node[draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (phi) at (0,-4) {$\phi$};
\node[shape=circle, draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (GA) at (-4.5,-4) {$G^A$};
\node[shape=circle, draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (GB) at (4.5,-4) {$G^B$};
\path [-stealth] (gamma) edge (delta);
\path [-stealth] (delta) edge (HA);
\path [-stealth] (delta) edge (HB);
\path [-stealth] (eta) edge (HA);
\path [-stealth] (eta) edge (HB);
\path [-stealth] (alpha) edge (HA);
\path [-stealth] (alpha) edge (HB);
\path [-stealth] (HA) edge (GA);
\path [-stealth] (HB) edge (GB);
\path [-stealth] (phi) edge (GA);
\path [-stealth] (phi) edge (GB);
\end{tikzpicture}
</script>
<i><font color="#0093af">Probabilistic graphical model for the decomposition of the data generation process illustrating the record linkage problem we tackle with a Stochastic EM.</font></i>
<br>
<br>
</div>
</div>

<br>
To wit, the parameter $$\eta$$ aligns with the multinomial distribution of each PIV. From the observed registered data $$G^A$$ and $$G^B,$$ we generate underlying credible true values $$H^A$$ and $$H^B$$ factoring in potential missing values and mistakes with $$\phi.$$ By comparing the latent information generated for the records supposedly referring to the same entities, we account for changes between the information collected in file $$A$$ and in file $$B$$ with $$\alpha.$$ (The place of residence is likely to change through the years for instance). We then use blocking techniques to build plausible pairs, that are those which connect records when their true values agree together for stable PIVs (which are thought not to evolve over time). We evaluate the contribution of each candidate pair to the complete data likelihood and decide whether to accept or reject it. We finally fit the probability for a record in file $$A$$ to form a link with a record in file $$B$$ with $$\gamma.$$ We sketch the outline of the methodology in the probabilistic graphical model above.
