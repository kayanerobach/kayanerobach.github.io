---
layout: post
title: When random matrix theory meets theoretical ecology
date: 2022-11-27 11:46:00
description: Study of the phase transition phenomena for the feasibility, Volterra Lyapunov stability and P-property in Lotka Volterra models
tags: RMT TheoreticalEcology P-matrix LotkaVolterra
categories: sample-posts
thumbnail: assets/img/rmt_theoreticalecology.png
---

### Overview

This is an investigation on the P-property of the inverse of a random matrix under positive diagonal deformation. This project is driven by the objective of understanding properties of large dynamic Lotka Volterra systems equilibria for
theoretical ecology.

### Supporting information 

<br>
<div style="margin-left: 30px;">
  <a href="/assets/pdf/RMTreport.pdf" target="_blank" rel="noopener noreferrer">
    <i class="fa-solid fa-file-pen" title="Report" style="font-size: 74px;"></i>
  </a> 
</div>
<br>
<div style="margin-left: 30px;">
  <a href="/assets/pdf/RMTprez.pdf" target="_blank" rel="noopener noreferrer">
    <i class="fa-solid fa-file-image" title="Slides" style="font-size: 74px;"></i>
  </a> 
</div>
<br>

### From the P-property to regularity of an interval matrix

$$I_N - \Gamma_N \text{ P-matrix} \iff \left[ -2 {\Gamma_N}^{-1}, -2 {\Gamma_N}^{-1} + 2 I_N \right] \text{ is regular}$$

Matrices in this interval have the form: $$-2 {\Gamma_N}^{-1} + \Delta$$, where $$\Delta$$ is a diagonal matrix with entries in $$[0,2]$$.

The challenge consist in showing that the interval contains no singular matrix.

### Jiri Rohn's algorithm

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
    {% include repository/repo.liquid username='robachowyk' repository='robachowyk/RMTTheoreticalEcology' %}
</div>

Consider an exhaustive list of methods to determine the **REG**ular**I**ty or the **SING**ularity of the interval $$[A_c - \Delta, A_c + \Delta]$$ where $$A_c = (A - I)^{-1} (A + I)$$ and $$\Delta = I$$; $$A$$ being a matrix of size $$(n \times n)$$ and $$I$$ the identity matrix of size $$(n \times n)$$.

**Conditions for the existence of a singular matrix**

- *midpoint matrix* $$A_c$$: 
<br>
the midpoint matrix $$A_c$$ of the interval matrix $$[A_c \pm \Delta]$$ is singular.
    
- *diagonal condition* [Theorem 2.1 from Oettli and Prager](https://doi.org/10.1137/S0895479896310743): 
<br>
$$|A_c x| \leq \Delta |x|$$ has a non trivial (i.e. non zero) solution $$x$$.
    
- *steepest determinant descent* [Algorithm 5.1](https://doi.org/10.1016/0024-3795(89)90004-9): 
<br>
investigate determinant bounds of the interval matrix (i.e. the hull of matrices determinant for matrices in the interval).
    
- *two Qz-matrices* [Theorem 4.3](https://doi.org/10.1137/S0895479896313978): 
<br>
the linear programming problem $$(\star)$$ maximize $$z^T x$$ subject to $$(A_c - \Delta \cdot diag(z)) x \leq 0$$ and $$diag(z) \cdot x \geq 0$$, is unbounded for some $$z \in \{ \pm 1 \}^n$$.
    
- *main algorithm* [Theorem 2.2 - find the singular matrix](https://doi.org/10.1137/0614007): 
<br>
loop on $$\{ \pm 1 \}^n$$ to identify the possible singular matrix which should have the specific form.
    
- *symmetrization* [Sections 4 and 5 from Rex and Rohn](https://doi.org/10.1137/S0895479896310743): 
<br>
both of the following conditions imply the singularity of $$[A_c \pm \Delta]$$:
    - $$\lambda_{\max}({A_c}^T A_c) \leq \lambda_{\min}(\Delta^T \Delta)$$ (norm of $$\Delta$$ is larger)
    - $$\Delta^T \Delta - {A_c}^T A_c$$ positive definite 

**Conditions for the regularity of the interval**

- *Beeck's condition* [Corollary 3.2 from Beeck](https://doi.org/10.1137/S0895479896310743): 
<br>
$$\rho (|{A_c}^{-1}| \Delta)<1$$ is regular (for $$A_c$$ non singular).

- *symmetrization* [Sections 4 and 5 from Rex and Rohn](https://doi.org/10.1137/S0895479896310743): 
<br>
both of the following conditions imply the regularity of $$[A_c \pm \Delta]$$:
    - $$\lambda_{\max}(\Delta^T \Delta) < \lambda_{\min}({A_c}^T A_c)$$
    - $${A_c}^T A_c - | \Delta^T \Delta | I$$ is positive definite

- *two Qz-matrices* [Theorem 4.3](https://doi.org/10.1137/S0895479896313978): 
<br>
the linear programming problem $$(\star)$$ is bounded for all $$z \in \{ \pm 1 \}^n$$.  

- *main algorithm* [Theorem 2.2 - all matrices are non singular](https://doi.org/10.1137/0614007): 
<br>
loop on $$\{ \pm 1 \}^n$$ to check there is no singular matrix in the whole interval. This last track is the most expensive since the algorithm will investigate the values of the sign real spectral radius.

