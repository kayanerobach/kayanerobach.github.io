---
layout: post
title: Flex Test
date: 2025-09-29 11:34:00
description: test
tags: RecordLinkage, LatentVariables, StEM
categories: sample-posts
thumbnail: assets/img/FlexRL.png
tikzjax: true
---

### Overview

Combining data from various sources such as observational studies and municipality registries or hospital databases empowers researchers to explore innovative questions and improve models. However, the lack of a unique identifier often poses challenges. Natural problems like counting casualties require distinguishing individuals in registers that may contain duplicates when bodies are listed by several organisations. Conducting healthcare longitudinal studies require follow up information that is often concealed due to privacy considerations.

Record linkage procedures determine whether pairs of observations collected on different occasions belong to the same individual using partially identifying variables (e.g. initials, birth year, zipcode). The complexity of this problem stems from the sub-par reliability of the partially identifying variables used to link records and their limited number of unique values. Furthermore, because entities are often uniquely represented in each file, records from one file can maximally be linked with one record in the other file, making the linkage decisions interdependent.

We propose a Stochastic Expectation Maximisation to combine observations from two overlapping data sets, that adapts to varying data complexities, addressing registration errors, including mistakes and missing values, and accommodating changes of the identifying information over time. Taking account of zip code temporal dynamics holds importance in healthcare longitudinal studies; in the particular case of survival analysis, long term follow-up are crucial, which increases the probability to move.

...