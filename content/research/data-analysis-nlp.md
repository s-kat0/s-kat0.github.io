---
title: "Data Analysis and NLP for Practical Solutions"
date: 2026-10-23
draft: false
---

This research develops data analysis, machine learning, and natural language processing (NLP) methods for problems in manufacturing processes and materials, together with collaborators in industry, pharmaceutics, and medicine.

## Data-Driven Discovery of Constitutive Models

A constitutive equation relates the deformation of a fluid to its stress. Constitutive equations of complex fluids such as polymer solutions have been derived by researchers based on physical insight, and no systematic derivation procedure has been established. We proposed Rheo-SINDy, which applies sparse identification of nonlinear dynamics (SINDy) to rheological data. Rheo-SINDy expresses the time derivative of the stress as a linear combination of candidate functions of the stress and the velocity gradient, and sparse regression selects a small number of terms. The resulting constitutive equation is an explicit and interpretable formula [1]. This topic is part of our Japan Science and Technology Agency (JST) PRESTO project on autonomy-driven physical modeling (see [AutoPMoB](/research/autopmob/)).

{{< figure src="/images/research/rheo_sindy_schematic.png" width="513" alt="Schematic illustration of Rheo-SINDy" caption="Schematic illustration of Rheo-SINDy. Reproduced from T. Sato, S. Miyamoto, and S. Kato, Journal of Rheology, vol. 69, no. 1, pp. 15–34 (2025) under the CC BY 4.0 license." >}}

- **Shear flow.** For four models with known constitutive equations, the upper-convected Maxwell, Giesekus, Hookean dumbbell, and FENE-P dumbbell models (FENE: finitely extensible nonlinear elastic), Rheo-SINDy identified the correct equations or equations close to them from simulated data. For the FENE dumbbell model, which has no analytical constitutive equation, it derived an approximate equation that reproduces nonlinear shear properties at steady state, including shear thinning [1].
- **Extensional flow.** Under uniaxial, planar, and biaxial extensional flows, Rheo-SINDy identified the exact form of the Giesekus model. For the FENE dumbbell model, it derived an approximate equation with 14 terms that predicts the stress under steady uniaxial extension with a deviation of about 1% at an extension rate of 8 and about 8% at an extension rate of 30, which lies outside the range of the training data. The identified equation consists of three ordinary differential equations, whereas the original model requires stochastic simulation of many dumbbells [2].

## Multimodal AI for Understanding Process Knowledge

Knowledge for designing and operating process plants is spread across sources in different formats: piping and instrumentation diagrams (P&IDs), equations that describe physical and chemical phenomena, and technical documents. For example, the equipment tag "HX-101" in a P&ID, the variable *Q* in a heat balance, and the phrase "heat transfer rate in the heat exchanger" in a document can refer to the same physical quantity, but the correspondence is implicit and engineers have to connect such information manually. In our JST BOOST project (2026–2031), conducted with the Natural Language Processing Team of the Artificial Intelligence Research Center, National Institute of Advanced Industrial Science and Technology (AIST), we are developing a multimodal artificial intelligence (AI) foundation that understands diagrams, equations, and text together. The AI learns the correspondence among symbols in diagrams, variables in equations, and descriptions in text, organizes expert knowledge as a knowledge graph, and uses natural language generation to build physical models, explain their meaning, and answer questions from engineers. This work aims to support process design and the transfer of knowledge from experienced engineers.

In addition, in joint research with companies, we develop NLP methods for using in-house documents in manufacturing.

## Collaborative Research

- **Pharmaceutical continuous manufacturing.** The proactive-residence time distribution (P-RTD) method determines the setpoints of critical material attributes (CMAs) by predicting the CMAs at the outlet of a process with residence time distribution (RTD) functions. In simulations of a continuous dry granulation line under eight conditions, the CMAs stayed within the design space for the entire evaluation period only with the P-RTD method [3]. We also showed that soft sensors using only material attributes and mixer-independent process parameters predict tablet quality without reconstruction after mixer changes [4], and that heterogeneous transfer learning from batch manufacturing data reduces the prediction error of tablet hardness in continuous manufacturing by 9.36 N on average [5].

{{< figure src="/images/research/prtd_setpoint.png" alt="Example of setpoint determination with the P-RTD method" caption="Example of setpoint determination with the P-RTD method (DS: design space). Reproduced from P. H. Pathirannahalage et al., International Journal of Pharmaceutics, vol. 682, 125922 (2025) under the CC BY-NC 4.0 license." >}}

- **Transfer learning for process data.** Transfer learning methods based on generative adversarial networks (GANs) generate data for a new operating condition from data under previous conditions. For a chemical reaction process before and after a catalyst change, the method achieved higher prediction performance than models built only from data after the change [6, 7].
- **Medical and healthcare data.** Our collaborative studies include generation of disease-specific electrocardiogram (ECG) data with a diffusion model [8], prediction of postprandial maximum and minimum blood glucose levels in 56 people with diabetes with mean absolute errors of 29.7 mg/dL and 20.2 mg/dL [9], prediction of postoperative delirium from preoperative electroencephalogram and heart rate variability [10], and correction of R-R interval (RRI) data containing extrasystoles [11].

## References

1. T. Sato, S. Miyamoto, and S. Kato, "Rheo-SINDy: Finding a constitutive model from rheological data for complex fluids using sparse identification for nonlinear dynamics," Journal of Rheology, vol. 69, no. 1, pp. 15–34 (2025) doi: [10.1122/8.0000872](https://doi.org/10.1122/8.0000872)
2. T. Sato, S. Miyamoto, and S. Kato, "Development of Rheological Constitutive Modeling Method Using a Sparse Identification Algorithm: A Case Study for Extensional Flows," Nihon Reoroji Gakkaishi, vol. 54, no. 2, pp. 119–128 (2026) doi: [10.1678/rheology.54.119](https://doi.org/10.1678/rheology.54.119)
3. P. H. Pathirannahalage, A. Nabetani, S. Kato, K. Sato, K. Yaginuma, S. Tanabe, and M. Kano, "Proactive-residence time distribution method for determining low-risk setpoints of critical material attributes in pharmaceutical continuous manufacturing," International Journal of Pharmaceutics, vol. 682, 125922 (2025) doi: [10.1016/j.ijpharm.2025.125922](https://doi.org/10.1016/j.ijpharm.2025.125922)
4. Y. Kobayashi, S. Kim, T. Nagato, T. Oishi, S. Kato, and M. Kano, "Mixer-Independent Soft Sensors to Predict Tablet Critical Quality Attributes in a Continuous Direct Compression Process," Journal of Chemical Engineering of Japan, vol. 59, no. 1 (2026) doi: [10.1080/00219592.2026.2665936](https://doi.org/10.1080/00219592.2026.2665936)
5. Y. Kobayashi, T. Nagato, T. Oishi, S. Kim, S. Kato, and M. Kano, "Heterogeneous Transfer Learning from Batch to Continuous Direct Compression Tablet Manufacturing," IFAC-PapersOnLine, vol. 59, pp. 325–330 (2025) doi: [10.1016/j.ifacol.2025.07.166](https://doi.org/10.1016/j.ifacol.2025.07.166)
6. B. Wang, S. Kato, and M. Kano, "GAN-based Homogenous Transfer Learning Method for Regression Problems," 2023 IEEE CCTA, pp. 85–90 (2023) doi: [10.1109/CCTA54093.2023.10252827](https://doi.org/10.1109/CCTA54093.2023.10252827)
7. R. Yoshida, B. Wang, S. Kato, and M. Kano, "Transfer Learning Based on Generative Adversarial Networks: Application to Chemical Reaction Process," 2024 CoDIT, pp. 2676–2679 (2024) doi: [10.1109/CoDIT62066.2024.10708203](https://doi.org/10.1109/CoDIT62066.2024.10708203)
8. H. Chen, S. Kato, K. Eguchi, T. Kawaji, and M. Kano, "Classifier-Guided Diffusion Model for Generating Disease-Specific ECG Data: A Case Pilot Study on Inferior Myocardial Infarction," EMBC 2025, pp. 1–6 (2025) doi: [10.1109/EMBC58623.2025.11253197](https://doi.org/10.1109/EMBC58623.2025.11253197)
9. K. Nagayama et al., "Prediction of Maximum and Minimum Postprandial Blood Glucose Levels in People with Diabetes," APSIPA ASC 2025, pp. 1639–1644 (2025) doi: [10.1109/APSIPAASC65261.2025.11249145](https://doi.org/10.1109/APSIPAASC65261.2025.11249145)
10. S. Mito et al., "Postoperative Delirium Prediction Based on Preoperative Electrocardiogram and Electroencephalogram," APSIPA ASC 2024, pp. 1–5 (2024) doi: [10.1109/APSIPAASC63619.2025.10848992](https://doi.org/10.1109/APSIPAASC63619.2025.10848992)
11. S. Chen, S. Kato, K. Fujiwara, and M. Kano, "Nearest Neighbor Search-Based Modification of RRI Data with Premature Atrial Contraction and Premature Ventricular Contraction," 2023 SICE ISCS, pp. 53–57 (2023) doi: [10.23919/SICEISCS57194.2023.10079199](https://doi.org/10.23919/SICEISCS57194.2023.10079199)

See the [Publications](/publication-list/) page for the full list.
