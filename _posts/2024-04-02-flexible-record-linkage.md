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

This is an example post with blablabla

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
    \caption{Probabilistic graphical model for the decomposition of the data generation process illustrating the record linkage problem.}
\end{figure}
</script>
