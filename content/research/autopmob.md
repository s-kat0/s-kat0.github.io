---
title: "AutoPMoB: Automated Physical Model Builder"
date: 2026-10-21
draft: false
---

## Overview

To realize a digital twin in a chemical plant, it is necessary to have a physical model (first-principles model) that can accurately represent the actual process. However, physical model building requires trial and error by researchers with expertise, making it difficult and costly. We have been developing an artificial intelligence (AI) based system called AutoPMoB (automated physical model builder) that automatically constructs physical models from literature databases. Realizing AutoPMoB requires several elemental technologies, which we are developing using natural language processing and machine learning.

## Model Building Flow of AutoPMoB

AutoPMoB builds a desired physical model by 1) collecting documents on the target process, 2) unifying their formats, 3) extracting the information required for model building, 4) unifying the notation of the extracted information, and 5) integrating the information.

![Model building flow of AutoPMoB](/images/research/autopmob_flow_en.svg)

### Extraction of Information Required for Model Building

The information required for model building includes variables, equations, and experimental data. We are developing methods to extract this information accurately from documents, as well as tools to efficiently create the data needed to develop and validate the extraction methods.

### Equivalence Judgment of Extracted Information

Variables and equations are written differently across documents. To enable AutoPMoB to understand multiple documents, we are developing methods to judge whether pieces of extracted information represent the same meaning (equivalence).

### Building and Evaluation of Model Candidates

We are developing methods that integrate the extracted information to automatically build physical models based on chemical engineering knowledge.

## Related Publications

See the [Publications](/publication-list/) page for the main results.
