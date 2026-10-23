---
title: "実問題解決のためのデータ解析とNLP"
date: 2026-10-23
draft: false
---

製造プロセスや材料の課題を対象に，データ解析，機械学習，自然言語処理（NLP）の手法を開発している．企業，製薬，医療分野の共同研究者とも研究を進めている．

## データ駆動による構成方程式の発見

構成方程式は，流体の変形と応力の関係を表す式である．高分子溶液などの複雑流体の構成方程式は，研究者が物理的な洞察に基づいて導出してきたものであり，体系的な導出手順は確立されていない．私たちは，非線形力学のスパース同定（SINDy: sparse identification of nonlinear dynamics）をレオロジーデータに適用する Rheo-SINDy を提案した．Rheo-SINDy は，応力の時間微分を応力と速度勾配の候補関数の線形結合で表し，スパース回帰によって少数の項を選択する．得られる構成方程式は，解釈可能な陽な数式である [1]．このテーマは，科学技術振興機構（JST）さきがけで取り組む自律駆動型物理モデリングの一部である（[AutoPMoB](/ja/research/autopmob/) を参照）．

{{< figure src="/images/research/rheo_sindy_schematic.png" width="513" alt="Rheo-SINDyの模式図" caption="Rheo-SINDy の模式図．T. Sato, S. Miyamoto, and S. Kato, Journal of Rheology, vol. 69, no. 1, pp. 15–34 (2025) より CC BY 4.0 ライセンスに基づき転載．" >}}

- **せん断流動**：構成方程式が既知の 4 つのモデル（上随伴 Maxwell モデル，Giesekus モデル，Hooke ダンベルモデル，FENE-P ダンベルモデル．FENE は finitely extensible nonlinear elastic の略）について，シミュレーションデータから正しい式またはそれに近い式を同定した．解析的な構成方程式が存在しない FENE ダンベルモデルでは，ずり流動化を含む定常状態の非線形せん断特性を再現する近似式を導出した [1]．
- **伸長流動**：一軸・平面・二軸伸長流動において，Giesekus モデルの厳密な式を同定した．FENE ダンベルモデルでは 14 項からなる近似式を導出し，定常一軸伸長の応力を，伸長速度 8 で約 1%，学習データの範囲外の伸長速度 30 で約 8% の偏差で予測した．同定した式は 3 本の常微分方程式であり，多数のダンベルの確率的シミュレーションを必要とする元のモデルより簡潔に計算できる [2]．

## 製造プロセスの知識を理解するマルチモーダルAI

プロセスプラントの設計・運転に必要な知識は，配管計装図（P&ID: piping and instrumentation diagram），物理・化学現象を記述する数式，技術文書といった形式の異なる情報源に分散している．例えば，P&ID 上の装置記号「HX-101」，熱収支式中の変数 *Q*，技術文書中の「熱交換器における伝熱量」は同じ物理量を指しうるが，その対応関係は明示されておらず，技術者が人手で結び付けている．JST BOOST のプロジェクト（2026〜2031 年度）では，産業技術総合研究所 人工知能研究センターの自然言語処理チームと共同で，図面・数式・文章を統合的に理解するマルチモーダル人工知能（AI）基盤を開発している．この AI は，図中の記号，数式中の変数，文章中の説明の対応関係を学習し，専門知識を知識グラフとして体系化し，自然言語生成を用いて物理モデルの構築，モデルの意味の説明，技術者からの質問への回答を行う．これにより，プロセス設計の支援と，熟練者が持つ知識の継承に貢献することを目指している．

また，企業との共同研究で，製造業の社内文書を活用するための自然言語処理技術を開発している．

## 共同研究

- **医薬品連続生産**：proactive-residence time distribution（P-RTD）法は，滞留時間分布（RTD: residence time distribution）関数を用いて工程出口の重要物質特性（CMA: critical material attribute）を予測し，CMA の設定値を決める．連続乾式造粒ラインの 8 条件のシミュレーションにおいて，評価期間の全体で CMA をデザインスペース内に保ったのは P-RTD 法のみであった [3]．また，物質特性と混合機に依存しない操作条件のみを入力とするソフトセンサーが，混合機の変更後も再構築なしに錠剤品質を予測できること [4]，バッチ生産のデータを用いた異種ドメイン転移学習により，連続生産における錠剤硬度の予測誤差が平均 9.36 N 減少すること [5] を示した．

{{< figure src="/images/research/prtd_setpoint.png" alt="P-RTD法による設定値決定の例" caption="P-RTD 法による設定値決定の例（DS: デザインスペース）．P. H. Pathirannahalage et al., International Journal of Pharmaceutics, vol. 682, 125922 (2025) より CC BY-NC 4.0 ライセンスに基づき転載．" >}}

- **プロセスデータの転移学習**：敵対的生成ネットワーク（GAN）に基づく転移学習手法により，以前の運転条件のデータから新しい運転条件のデータを生成する．触媒変更前後の化学反応プロセスにおいて，変更後のデータのみで構築したモデルより高い予測性能を達成した [6, 7]．
- **医療・ヘルスケアデータ**：拡散モデルによる疾患特異的な心電図（ECG）データの生成 [8]，糖尿病患者 56 名の食後最高・最低血糖値の予測（平均絶対誤差 29.7 mg/dL・20.2 mg/dL）[9]，術前の脳波と心拍変動からの術後せん妄の予測 [10]，期外収縮を含む R-R 間隔（RRI）データの修正 [11] に共同で取り組んでいる．

## 参考文献

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

全業績は[研究業績](/ja/publication-list/)を参照．
