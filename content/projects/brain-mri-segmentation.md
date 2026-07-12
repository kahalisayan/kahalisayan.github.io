---
title: "Brain MRI Segmentation and Bias-Field Correction"
summary: "Volumetric brain MRI segmentation combining fuzzy clustering, intensity-inhomogeneity modelling, and multi-objective optimization."
status: "Published"
weight: 30
theme: "Medical Image Segmentation"
tags: ["brain MRI", "segmentation", "fuzzy clustering", "bias-field correction"]
publications: ["kahali2016biasfield", "kahali2017twostage", "kahali2017convolution", "mahata2018local", "kahali2019entropy"]
---

## Overview

Doctoral and follow-on work on volumetric brain MRI segmentation and correction of
intensity inhomogeneity (bias field). The methods combine fuzzy clustering,
Gaussian-surface and polynomial bias-field modelling, entropy-based likelihood
measures, and multi-objective optimization for 3D brain MR image data.

## Motivation

Reliable brain MRI segmentation is complicated by intensity inhomogeneity and partial
volume effects. Modelling the bias field explicitly, and incorporating local
contextual information, improves both segmentation and inhomogeneity estimation.

## Research questions

- How should the bias field be modelled — polynomial or Gaussian surface fitting —
  for accurate estimation and correction?
- Can segmentation and intensity-inhomogeneity estimation be performed simultaneously?
- How can entropy-based and contextual information improve fuzzy c-means clustering
  for brain MR data?

## Approach

A two-stage multi-objective segmentation framework; convolution of 3D Gaussian
surfaces for volumetric inhomogeneity estimation; and entropy-based fuzzy c-means
clustering with local contextual information.

## Key outputs

Published in *Journal of Chemometrics*, *Applied Soft Computing*, *IET Computer
Vision*, and *Soft Computing*, with related conference papers. See the linked
publications below.

## Status

Published. Related publications are listed on the
[Publications](/publications/) page.
