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

This is an example post with TikZ code. TikZJax converts script tags (containing TikZ code) into SVGs.

<script type="text/tikz">
\begin{tikzpicture}
    \draw[red,fill=black!60!red] (0,0) circle [radius=1.5];
    \draw[green,fill=black!60!green] (0,0) circle [x radius=1.5cm, y radius=10mm];
    \draw[blue,fill=black!60!blue] (0,0) circle [x radius=1cm, y radius=5mm, rotate=30];
\end{tikzpicture}
</script>

Combining data from various sources such as observational studies and municipality registries or hospital databases empowers researchers to explore innovative questions and improve models. However, the lack of a unique identifier often poses challenges. Natural problems like counting casualties require distinguishing individuals in registers that may contain duplicates when bodies are listed by several organisations. Conducting healthcare longitudinal studies require follow up information that is often concealed due to privacy considerations.

Record linkage procedures determine whether pairs of observations collected on different occasions belong to the same individual (referred to as links) using partially identifying variables (e.g. initials, birth year, zipcode). The complexity of this problem stems from the sub-par reliability of those variables and their low discriminative power, due to limited unique values. Furthermore, since everyone is often uniquely represented in each file, records from one file can maximally be linked with one record in the other file. Linkage decisions are thus interdependent, adding complexity to the task.

Existing methodologies typically involve a compromise between computational efficiency and accuracy. Traditional approaches simplify this task by condensing information, yet they neglect dependencies among linkage decisions and disregard the one-to-one relationship required to establish coherent links. Modern approaches offer a comprehensive representation of the data generating process, at the expense of substantial computational overhead and reduced flexibility.

<div align=center>
<script type="text/tikz">
\begin{tikzpicture}
\node[draw=black, minimum size=1cm] (gamma) at (0,4) {$\gamma$};
\node[draw=black, dashed, minimum size=1cm] (delta) at (0,2) {$\Delta$};
\node[draw=black, minimum size=1cm] (eta) at (0,0) {$\eta$};
\node[draw=black, minimum size=1cm] (alpha) at (0,-2) {$\alpha$};
\node[shape=circle, dashed, draw=black, minimum size=1cm] (HA) at (-3,-2) {$H_A$};
\node[shape=circle, dashed, draw=black, minimum size=1cm] (HB) at (3,-2) {$H_B$};
\node[draw=black, minimum size=1cm] (phi) at (0,-4) {$\phi$};
\node[shape=circle, draw=black, minimum size=1cm] (GA) at (-4.5,-4) {$G_A$};
\node[shape=circle, draw=black, minimum size=1cm] (GB) at (4.5,-4) {$G_B$};
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
*Probabilistic graphical model for the decomposition of the data generation process illustrating the record linkage problem we tackle with a Stochastic EM.*
</div>

This project proposes a flexible method to determine the set of links, that adapts to varying data complexities, addressing registration errors, including inaccuracies and missing values, and accommodating changes of the identifying information over time. Addressing temporal dynamics of zipcode for instance holds importance in healthcare longitudinal studies. In the particular case of survival analysis long term follow-up are crucial, which increases the probability to move. Our approach balances computational scalability and accuracy, estimating the linkage by maximum likelihood using a Stochastic Expectation Maximisation algorithm on a latent variable model.

In the paper, we illustrate the ability of our methodology to connect observations using two large real data applications and demonstrate the robustness of our model to the linking variables quality in a simulation study.

The proposed algorithm FlexRL is available in R and the code is available on github, as well as complementary materials:

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
    {% include repository/repo.liquid username='robachowyk' repository='robachowyk/RecordLinkage' %}
</div>

<script type="text/tikz">
\begin{figure}
    \centering
    \begin{tikzpicture}

        \node[draw, minimum size=1cm] (gamma) at (0,4) {$\gamma$};
        \node[shape=circle, dashed, draw, minimum size=1cm] (delta) at (0,2) {$\boldsymbol{\Delta}$};
        \node[draw, minimum size=1cm] (eta) at (0,0) {$\boldsymbol{\eta}$};
        \node[draw, minimum size=1cm] (alpha) at (0,-2) {$\boldsymbol{\alpha}$};
        \node[shape=circle, dashed, draw, minimum size=1cm] (HA) at (-3,-2) {$\textbf{H}^{\mathcal{A}}$};
        \node[shape=circle, dashed, draw, minimum size=1cm] (HB) at (3,-2) {$\textbf{H}^{\mathcal{B}}$};
        \node[draw, minimum size=1cm] (phi) at (0,-4) {$\boldsymbol{\phi}$};
        \node[shape=circle, draw, minimum size=1cm] (GA) at (-4.5,-4) {$\textbf{G}^{\mathcal{A}}$};
        \node[shape=circle, draw, minimum size=1cm] (GB) at (4.5,-4) {$\textbf{G}^{\mathcal{B}}$};

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

        \plate [inner sep=.5cm, yshift=.2cm] {data A} {(HA)(GA)} {$i = 1, \dots, \nA$};
        \plate [inner sep=.5cm, yshift=.2cm] {data B} {(HB)(GB)} {$j = 1, \dots, \nB$};
        \plate [inner sep=.25cm, yshift=.2cm] {data linked} {(HA)(alpha)(HB)} {$(i,j)$};
    \end{tikzpicture}
    \caption{Probabilistic graphical model for the decomposition of the data generation process illustrating the record linkage problem we tackle with a Stochastic EM.}
\end{figure}
</script>
