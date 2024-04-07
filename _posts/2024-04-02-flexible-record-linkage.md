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

Record linkage procedures determine whether pairs of observations collected on different occasions belong to the same individual (referred to as links) using partially identifying variables (e.g. initials, birth year, zipcode). The complexity of this problem stems from the sub-par reliability of those variables and their low discriminative power, due to limited unique values. Furthermore, since everyone is often uniquely represented in each file, records from one file can maximally be linked with one record in the other file. Linkage decisions are thus interdependent, adding complexity to the task.

Existing methodologies typically involve a compromise between computational efficiency and accuracy. Traditional approaches simplify this task by condensing information, yet they neglect dependencies among linkage decisions and disregard the one-to-one relationship required to establish coherent links. Modern approaches offer a comprehensive representation of the data generating process, at the expense of substantial computational overhead and reduced flexibility.

This project proposes a flexible method to determine the set of links, that adapts to varying data complexities, addressing registration errors, including inaccuracies and missing values, and accommodating changes of the identifying information over time. Taking account of zip code temporal dynamics for instance holds importance in healthcare longitudinal studies; in the particular case of survival analysis long term follow-up are crucial, which increases the probability to move.

To estimate the linkage, we build a statistical model that leverages the latent representation ($H^A$ and $H^B$) of the partially identifying information embedded in the data generation process ($G^A$ and $G^B$), and ultimately derive a linkage estimate 
$$
\Delta.
$$
We estimate the model parameters: 
$$
\gamma, \eta, \alpha, \phi,
$$
represented as input nodes on the probabilistic graphical model above, using a Stochastic Expectation Maximisation algorithm. We sketch the outline of the methodology hereafter:
<br>

<div align=center>
<script type="text/tikz">
\begin{tikzpicture}
\node[draw={rgb:red,0;green,147;blue,175}, minimum size=1cm] (gamma) at (0,4) {$\textcolor{blue}{\gamma}$};
\node[draw, dashed, minimum size=1cm] (delta) at (0,2) {$\Delta$};
\node[draw, minimum size=1cm] (eta) at (0,0) {$\eta$};
\node[draw, minimum size=1cm] (alpha) at (0,-2) {$\alpha$};
\node[shape=circle, dashed, draw, minimum size=1cm] (HA) at (-3,-2) {$H^A$};
\node[shape=circle, dashed, draw, minimum size=1cm] (HB) at (3,-2) {$H^B$};
\node[draw, minimum size=1cm] (phi) at (0,-4) {$\phi$};
\node[shape=circle, draw, minimum size=1cm] (GA) at (-4.5,-4) {$G^A$};
\node[shape=circle, draw, minimum size=1cm] (GB) at (4.5,-4) {$G^B$};
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
<i>Probabilistic graphical model for the decomposition of the data generation process illustrating the record linkage problem we tackle with a Stochastic EM.</i>
</div>

<br>
In the paper, we illustrate the ability of our methodology to connect observations using two large real data applications and demonstrate the robustness of our model to the linking variables quality in a simulation study.

The proposed algorithm FlexRL is available in R and the code is available on github, as well as complementary materials:

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
    {% include repository/repo.liquid username='robachowyk' repository='robachowyk/RecordLinkage' %}
</div>
