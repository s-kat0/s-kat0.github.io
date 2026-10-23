---
title: "AutoPMoB: Automated Physical Model Builder"
date: 2026-10-23
draft: false
---

## Overview

A digital twin of a manufacturing process requires a physical model (first-principles model) that represents the actual process. Building such a model has relied on experts who search the literature and combine equations by trial and error. We are developing AutoPMoB (automated physical model builder), an artificial intelligence (AI) system that builds physical models from the literature on a target process. AutoPMoB retrieves documents on the target process, extracts the information required for model building, such as variables, equations, and experimental data, unifies the expressions of the information across documents, and builds, validates, and ranks model candidates [6].

{{< figure src="/images/research/autopmob_overview.png" alt="Schematic diagram of AutoPMoB" caption="Schematic diagram of AutoPMoB. Reproduced from S. Kato and M. Kano, Computer Aided Chemical Engineering, vol. 53, pp. 2839–2844 (2024). © 2024 Elsevier B.V." >}}

We built an AutoPMoB prototype that combines a large language model (LLM) with our model building algorithm and applied it to nine papers on a continuous stirred tank reactor (CSTR). The prototype extracted variable definitions with an accuracy of 74.1% and a recall of 95.3% and built physical models from the extracted information. The prototype also identified the tasks required for practical use: unifying notation across documents, retrieving relevant documents, and integrating information outside documents [6].

## Current Projects

The following projects extend AutoPMoB from text to multimodal information and from model building to the cycle of modeling and experimentation.

- **Japan Science and Technology Agency (JST) PRESTO, "Establishing Foundations for Autonomy-Driven Physical Modeling Using Multimodal Data" (2025–2029).** This project integrates knowledge extracted from the literature with a small amount of experimental data. It combines symbolic regression constrained by the extracted knowledge, evaluation of models from equations, plots, and natural language explanations, and the proposal of new experimental conditions. The framework is validated on a CSTR, polymer rheology, and the Czochralski crystal growth process.
- **JST BOOST (2026–2031).** This project develops a multimodal AI foundation that understands diagrams, equations, and text on manufacturing processes, toward the generation of physical models and the transfer of process knowledge (see [Data Analysis and NLP](/research/data-analysis-nlp/)).
- **Japan Society for the Promotion of Science (JSPS) Grant-in-Aid for Early-Career Scientists (2026–2029).** This project extends and systematizes the methods of AutoPMoB using LLMs.
- **National Institute of Advanced Industrial Science and Technology (AIST) KAKUSEI project (2025–2026).** This project evaluates the meaning of physical models using natural language, figures, and tables, and constructs an environment for active modeling.

## Model Building from Extracted Equations

Equations extracted from the literature include redundant, intermediate, and inconsistent equations. We formulated model building as the selection of combinations of equations that satisfy four requirements: inclusion of the required variables, consistency of the degrees of freedom, solvability, and uniqueness of constant equations. The proposed refined gradual method found all correct models (recall 1.00) in all eight case studies, including noisy equation sets and a CSTR with three components and two reactions; the previous gradual method found none of the correct models in two of the cases. The computational time depends on the structure of the equation set: in one case, the proposed method finished in 3.94 × 10⁻⁵ s, whereas exhaustive search took 14.8 s. For the largest set (29 equations with 1,024 correct models), exhaustive search was faster, and the paper provides guidelines for choosing a method according to the structure of the equation set [1]. The code is available on [GitHub](https://github.com/humansys-lab/preq-pmob).

## Extraction of Information Required for Model Building

Methods for extracting variables and their definitions from papers require annotated datasets, which did not exist for chemical engineering. We developed VARAT (variable annotation tool), which extracts variable symbols from documents and supports the annotation of their definitions. The symbol extraction algorithm achieved a recall of 97% and a precision of 96% on 47 papers on five manufacturing processes. With VARAT, we created a dataset of 1,988 variable symbols, and the annotation time per paper decreased from more than one hour to about 30 minutes [3].

{{< figure src="/images/research/varat_framework.png" alt="Framework of annotation using VARAT" caption="Framework of annotation using VARAT. Reproduced from S. Kato and M. Kano, Journal of Chemical Engineering of Japan, vol. 58, no. 1, 2454461 (2025) under the CC BY 4.0 license." >}}

Using this dataset, we develop methods for variable definition extraction, i.e., extracting the definition of a given variable symbol from a sentence.

- **Two-stage fine-tuning.** A BERT (Bidirectional Encoder Representations from Transformers) model is first fine-tuned on description patterns common to multiple fields and then on chemical process documents. The method outperformed single-stage fine-tuning for four of five BERT models, and DeBERTaV3-large reached an accuracy of 85.4% and an F1 score of 84.0% with limited training data [5].
- **Data augmentation with template sentences.** New training sentences are generated by filling template sentences with variable–definition pairs. The model trained with the generated sentences achieved an accuracy of 88.3%, 2.5 percentage points higher than the existing method, and also improved the accuracy on processes not included in the training data [7].

## Equivalence Judgment of Extracted Information

Different papers write the same variable or equation in different ways, and AutoPMoB has to judge whether two pieces of extracted information represent the same thing.

- **Equation groups.** We developed an algorithm that judges whether two groups of differential-algebraic equations can be transformed into the same form, using a computer algebra system. The algorithm eliminates variables that appear in only one equation group and then compares the solutions of the equations one by one. It judged all 50 test pairs correctly [2].
- **Variable definitions.** We built ProcessBERT, a language model pre-trained on about 130,000 papers on chemical engineering, and judged the equivalence of two definitions from the cosine similarity of their embeddings. ProcessBERT achieved a ROC-AUC (area under the receiver operating characteristic curve) of 0.925, higher than BERT (0.905) and SciBERT (0.877) [4].

{{< figure src="/images/research/equivalence_judgment.png" width="480" alt="Algorithm for judging the equivalence of two equation groups" caption="Algorithm for judging the equivalence of two equation groups (EG: equation group). Reproduced from S. Kato, C. Zhang, and M. Kano, Scientific Reports, vol. 13, 11534 (2023) under the CC BY 4.0 license." >}}

## References

1. S. Kato and M. Kano, "Automated physical model building from literature sources: Combining equations based on four predefined requirements," Computers & Chemical Engineering, vol. 200, 109147 (2025) doi: [10.1016/j.compchemeng.2025.109147](https://doi.org/10.1016/j.compchemeng.2025.109147)
2. S. Kato, C. Zhang, and M. Kano, "Simple algorithm for judging equivalence of differential-algebraic equation systems," Scientific Reports, vol. 13, 11534 (2023) doi: [10.1038/s41598-023-38254-y](https://doi.org/10.1038/s41598-023-38254-y)
3. S. Kato and M. Kano, "VARAT: Variable Annotation Tool for Documents on Manufacturing Processes," Journal of Chemical Engineering of Japan, vol. 58, no. 1, 2454461 (2025) doi: [10.1080/00219592.2025.2454461](https://doi.org/10.1080/00219592.2025.2454461)
4. S. Kato, K. Kanegami, and M. Kano, "ProcessBERT: A Pre-trained Language Model for Judging Equivalence of Variable Definitions in Process Models," IFAC-PapersOnLine, vol. 55, no. 7, pp. 957–962 (2022) doi: [10.1016/j.ifacol.2022.07.568](https://doi.org/10.1016/j.ifacol.2022.07.568)
5. S. Kato, M. Yamamoto, K. Nagayama, and M. Kano, "Two-Stage Fine-Tuning for Variable Definition Extraction from Chemical Process-related Papers," DAFUSAI 2024 [PDF](/pdf/DAFUSAI2024_kato.pdf)
6. S. Kato and M. Kano, "Prototype of Automated Physical Model Builder: Challenges and Opportunities," Computer Aided Chemical Engineering, vol. 53, pp. 2839–2844 (2024) doi: [10.1016/B978-0-443-28824-1.50474-9](https://doi.org/10.1016/B978-0-443-28824-1.50474-9)
7. K. Nagayama, S. Kato, and M. Kano, "Data Augmentation Method Utilizing Template Sentences for Variable Definition Extraction," NLDB 2024, pp. 151–165 (2024) doi: [10.1007/978-3-031-70239-6_11](https://doi.org/10.1007/978-3-031-70239-6_11)

See the [Publications](/publication-list/) page for the full list.
