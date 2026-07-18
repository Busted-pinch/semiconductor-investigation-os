# Complete Research Paper List — Domain Foundations
## FYP: Agentic Wafer Defect Root Cause Analysis with Counterfactual XAI

---

> **How to use this list:**
> Papers are grouped into 7 pillars that mirror your project's architecture. Each paper has a **WHY** (what it gives you), a **WHAT TO EXTRACT** (the exact knowledge to pull out), and an **ACCESS** link. Study every paper in Pillars 1–3 before writing a single line of code. Pillars 4–7 are for when you start building each module.

---

## PILLAR 1 — Wafer Defect Patterns: The Core Domain
*These papers define the problem space. They teach you what defect patterns are, how they form, and what they mean for process engineers. Without mastering these, your XAI outputs will have no physical meaning.*

---

### 1.1 ★★★ THE ORIGINAL WM-811K PAPER — Must Read First
**"Wafer Map Failure Pattern Recognition and Similarity Ranking for Large-Scale Data Sets"**
Wu, Jang, Chen — *IEEE Transactions on Semiconductor Manufacturing*, 2015

- **WHY:** This is the paper that created your training dataset. It defines the 8 defect classes, explains why spatial patterns matter, and establishes the benchmark everyone else builds on.
- **WHAT TO EXTRACT:** The exact definition of each defect class, the labeling methodology, the dataset split, and why only 3.1% of the 811K wafers are labeled.
- **ACCESS:** https://ieeexplore.ieee.org/document/6932449 (Search: "Wu Jang Chen 2015 wafer map failure pattern recognition IEEE TSM")

---

### 1.2 ★★★ Defect Pattern → Process Root Cause Mapping
**"Wafer Map Failure Pattern Classification Using Geometric Transformation-Invariant CNN"**
*Scientific Reports*, 2023

- **WHY:** This paper explicitly states which process step each WM-811K defect class comes from. This is the domain knowledge your Counterfactual Agent's knowledge base must be built on.
- **WHAT TO EXTRACT:** Table 1 — the mapping of Center/Donut/Edge-Loc/Edge-Ring/Scratch/Local/Near-Full/Random to specific process parameters and failure modes. Quote this in your project report.
- **ACCESS:** https://www.nature.com/articles/s41598-023-34147-2

---

### 1.3 ★★★ Defect Pattern → Root Cause — Quantum Paper Table (Best Table Available)
**"Bridging Quantum Computing Paradigms toward Semiconductor Yield: A Controlled CV-versus-DV Comparison on Wafer-Map Defect Classification"**
*arXiv*, 2025

- **WHY:** Contains the most detailed publicly available table (Table 1) mapping all 8 WM-811K defect patterns to their process root causes with primary references. Ignore the quantum computing part — this table alone is worth reading.
- **WHAT TO EXTRACT:** Table 1. Each row: defect class → process root cause → responsible process module → cited source.
- **ACCESS:** https://arxiv.org/pdf/2607.00961

---

### 1.4 ★★★ Spatial Signature Analysis — The Foundational Industry Paper
**"A Neural-Network Approach to Recognize Defect Spatial Patterns in Semiconductor Manufacturing"**
Chen & Liu — *Expert Systems with Applications*, 2000

- **WHY:** This is the paper that first established that spatial defect patterns (SSA) carry root cause information. It is cited by nearly every wafer map paper written since. Understanding SSA is essential for understanding WHY your CNN can imply root causes.
- **WHAT TO EXTRACT:** The concept of "spatial signature" — how a wafer's defect distribution shape encodes which process went wrong. The defect-to-process mapping used in this paper is the domain knowledge behind your whole system.
- **ACCESS:** Search "Chen Liu 2000 neural network defect spatial pattern semiconductor Expert Systems Applications"

---

### 1.5 ★★ Defect Pattern Taxonomy
**"Development of a Spatial Dimension-Based Taxonomy for Classifying Defect Patterns in a Wafer Bin Map"**
*Advanced Engineering Informatics*, 2024

- **WHY:** Gives you a formal, principled taxonomy of defect patterns. Your project report's background section needs to describe these patterns precisely. This paper gives you the vocabulary.
- **WHAT TO EXTRACT:** The 3 desirable properties of a good defect taxonomy; how defect patterns are classified by spatial dimension; why the same visual pattern can have different root causes depending on its spatial location.
- **ACCESS:** https://www.sciencedirect.com/science/article/abs/pii/S1474034624001885

---

### 1.6 ★★ Mixed-Type Defects — Beyond WM-811K
**"Semantic Segmentation-Based Wafer Map Mixed-Type Defect Pattern Recognition"**
*IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems*, 2023

- **WHY:** In real fabs, wafers often have more than one defect type at the same time (e.g., Edge-Ring + Scratch). WM-811K has only single-type labels, but MixedWM38 has 38 combined classes. This paper shows how real defects are more complex than your training data — important for your limitations section.
- **WHAT TO EXTRACT:** Why mixed-type defects make root cause analysis harder; the MixedWM38 dataset structure; how semantic segmentation differs from classification for this problem.
- **ACCESS:** https://ieeexplore.ieee.org/document/10122621/

---

### 1.7 ★★ Review of All Wafer Defect Detection Methods
**"Review of Wafer Defect Detection in Semiconductor Manufacturing: Algorithms, Systems, and Data"**
*Journal of Intelligent Manufacturing*, 2026

- **WHY:** The most up-to-date comprehensive survey of ALL wafer defect detection methods — from statistical methods to CNNs to transformers. This is your literature survey backbone.
- **WHAT TO EXTRACT:** The taxonomy of existing methods; where CNN-based classification sits relative to anomaly detection, segmentation, and retrieval methods; the open challenges section — this is where you position your innovation.
- **ACCESS:** https://link.springer.com/article/10.1007/s10845-026-02845-z

---

## PILLAR 2 — CNN Architecture & Visual Classification
*These papers teach you the deep learning backbone your Vision Agent runs on.*

---

### 2.1 ★★★ ResNet — The Architecture You Are Implementing
**"Deep Residual Learning for Image Recognition"**
He, Zhang, Ren, Sun — *CVPR*, 2016

- **WHY:** ResNet-18 is your proposed CNN backbone. This is the paper that invented it. You will cite this in every section of your project report.
- **WHAT TO EXTRACT:** The residual/skip connection mechanism; why very deep networks fail without shortcuts (vanishing gradient problem); the ResNet-18 architecture specifically (layer counts, filter sizes, parameter count); the ImageNet accuracy results.
- **ACCESS:** https://arxiv.org/abs/1512.03385

---

### 2.2 ★★★ GradCAM — The Visual XAI You Are Implementing
**"Grad-CAM: Visual Explanations from Deep Networks via Gradient-Based Localization"**
Selvaraju, Cogswell, Das, Vedantam, Parikh, Batra — *ICCV 2017 / IJCV 2019*

- **WHY:** GradCAM is the direct implementation component of your Vision Agent. You are implementing GradCAM++, which is an improvement of this. You cannot implement GradCAM++ without fully understanding the original.
- **WHAT TO EXTRACT:** The exact algorithm — how gradients from the last convolutional layer are pooled and multiplied with activation maps to produce a heatmap; the difference from CAM (no need for GAP layers); the guided GradCAM extension.
- **ACCESS:** https://arxiv.org/abs/1610.02391

---

### 2.3 ★★★ GradCAM++ — The Exact Method You Implement
**"Grad-CAM++: Generalized Gradient-Based Visual Explanations for Deep Convolutional Networks"**
Chattopadhyay, Sarkar, Howlader, Balasubramanian — *IEEE WACV*, 2018

- **WHY:** This is the exact method you said you are implementing — not GradCAM but GradCAM++. The improvement: uses weighted combinations of positive partial derivatives (second/third-order gradients) instead of global average pooling. Better localization when multiple instances of a class appear. For wafer defects spread across a region, this matters.
- **WHAT TO EXTRACT:** The mathematical formulation — specifically the pixel-wise weighting coefficients α; why it outperforms GradCAM for multi-object or partial-object scenarios; the ADCC (Average Drop, Coherency, Confidence) evaluation metric.
- **ACCESS:** https://arxiv.org/abs/1710.11063 (Search: "Chattopadhyay Grad-CAM++ 2018 WACV")

---

### 2.4 ★★ CNN-Based Transfer Learning for Wafer Defect Classification
**"A CNN-Based Transfer Learning Method for Defect Classification in Semiconductor Manufacturing"**
Imoto, Nakai, Ike, Haruki, Sato — *IEEE Transactions on Semiconductor Manufacturing*, 2019

- **WHY:** Shows exactly how transfer learning (pretrained ImageNet CNN → fine-tuned on wafer maps) works in the semiconductor context. This validates your ResNet-18 fine-tuning strategy.
- **WHAT TO EXTRACT:** How many layers to freeze vs. fine-tune; the accuracy vs. training data size tradeoff; why ImageNet-pretrained features transfer to wafer maps despite the domain difference.
- **ACCESS:** https://ieeexplore.ieee.org/document/8828022

---

### 2.5 ★★ Wafer Defect Classification with CNN + XAI — Direct Application
**"Advancing Semiconductor Fabrication: A CNN-Based Wafer Defect Detection with XAI Insights"**
*ResearchGate*, 2025

- **WHY:** One of the few papers that directly applies both CNN classification AND GradCAM visual explanation to wafer maps. Very close to your Vision Agent. Read this to understand what has already been done and where you go further.
- **WHAT TO EXTRACT:** The GradCAM visualization for center defects; the confusion matrix between similar-looking defect types (Edge-Loc vs. Scratch); the classification accuracy on 9 defect categories.
- **ACCESS:** https://www.researchgate.net/publication/392224877

---

### 2.6 ★★ Enhancing CNN Interpretability with LIME on Wafer Maps
**"Enhancing Confidence and Interpretability of a CNN-Based Wafer Defect Classification Model Using Temperature Scaling and LIME"**
Lee, Ju, Lim, Hong, Baek, Lee — *Micromachines*, 2025

- **WHY:** Directly applies LIME to wafer map CNN classification. This is your closest prior work in the XAI-on-wafer-maps domain. Your work goes further by adding counterfactuals and process correlation.
- **WHAT TO EXTRACT:** How LIME highlights which spatial regions of a wafer map the model uses; the temperature scaling method for calibrating confidence scores; comparison of LIME vs GradCAM explanations on the same wafer maps.
- **ACCESS:** https://www.mdpi.com/2072-666X/16/9/1057

---

### 2.7 ★ Attention Mechanism for Wafer Defect Detection
**"Wafer Map Defect Pattern Detection Method Based on Improved Attention Mechanism"**
*Expert Systems with Applications*, 2023

- **WHY:** Attention mechanisms like CBAM can improve your CNN's sensitivity to specific spatial regions — important for small defect clusters that GradCAM might miss.
- **WHAT TO EXTRACT:** How channel attention and spatial attention are implemented; when attention outperforms standard ResNet; the dual-branch architecture for handling mixed-type defects.
- **ACCESS:** https://www.sciencedirect.com/science/article/abs/pii/S0957417423010461

---

## PILLAR 3 — Explainable AI: Counterfactual, Feature Attribution, Theory
*These papers are the intellectual backbone of your XAI innovation. Every member of the team must understand these deeply.*

---

### 3.1 ★★★ DiCE — Your Counterfactual Implementation Framework
**"Explaining Machine Learning Classifiers through Diverse Counterfactual Explanations"**
Mothilal, Sharma, Tan — *ACM FAccT*, 2020

- **WHY:** DiCE is explicitly named in your proposal as the method you are adapting. This paper defines: what a counterfactual explanation is, how diversity and proximity are balanced, the loss function you will optimize, and why feasibility constraints matter. This is not optional — it is your implementation reference.
- **WHAT TO EXTRACT:** The optimization objective function (Equation 1 in the paper); the diversity term; the proximity term; the feasibility constraint formulation; the difference between DiCE-random, DiCE-KD, and DiCE-genetic backends.
- **ACCESS:** https://dl.acm.org/doi/10.1145/3351095.3372850 | Free PDF: https://arxiv.org/abs/1905.07697

---

### 3.2 ★★★ Counterfactual Explanations — The Foundational Theory
**"Counterfactual Explanations Without Opening the Black Box: Automated Decisions and the GDPR"**
Wachter, Mittelstadt, Russell — *Harvard Journal of Law and Technology*, 2017

- **WHY:** This is the paper that defined what a counterfactual explanation IS in the ML context. DiCE builds on this. Read this first to understand the theoretical foundation: "What is the smallest change to input X that would flip the model's output?" This defines the mathematical objective your counterfactual agent optimizes.
- **WHAT TO EXTRACT:** The formal definition of a counterfactual (Definition 1); why counterfactuals are legally meaningful (the "right to explanation" in GDPR); the proximity metric; the key limitation: proximity does not guarantee feasibility.
- **ACCESS:** https://arxiv.org/abs/1711.00399

---

### 3.3 ★★★ SHAP — Unified Feature Attribution
**"A Unified Approach to Interpreting Model Predictions" (SHAP)**
Lundberg, Lee — *NeurIPS*, 2017

- **WHY:** SHAP is used for your process parameter importance ranking — identifying which of your 6 IoT parameters contributed most to a defect. Your Process Correlation Agent needs a method to say "gas flow contributed 60% to this edge ring, temperature 30%." SHAP provides this.
- **WHAT TO EXTRACT:** The SHAP value formulation; why SHAP is theoretically grounded in game theory (Shapley values); how SHAP is applied to tabular sensor data; the difference between TreeSHAP (fast) and KernelSHAP (model-agnostic).
- **ACCESS:** https://arxiv.org/abs/1705.07874

---

### 3.4 ★★★ LIME — Local Interpretable Model-Agnostic Explanations
**"Why Should I Trust You?: Explaining the Predictions of Any Classifier"**
Ribeiro, Singh, Guestrin — *KDD*, 2016

- **WHY:** LIME is listed in your proposal's technology stack and literature review. It is the baseline XAI method against which you compare your GradCAM++ approach. Understanding how LIME creates local linear approximations is essential for explaining why GradCAM++ is more appropriate for image data.
- **WHAT TO EXTRACT:** The perturbation-based local approximation algorithm; LIME for image classification (superpixel masking); why LIME is unstable for images (random superpixel boundaries); why GradCAM is preferred for CNNs over LIME.
- **ACCESS:** https://arxiv.org/abs/1602.04938

---

### 3.5 ★★★ Comprehensive XAI Survey — Your Literature Survey Foundation
**"Explainable Artificial Intelligence (XAI): Concepts, Taxonomies, Opportunities and Challenges toward Responsible AI"**
Arrieta et al. — *Information Fusion*, 2020

- **WHY:** The definitive survey paper on all XAI methods — 250+ pages, 400+ citations. This is your primary reference for the XAI background chapter of your report. It categorizes LIME, SHAP, GradCAM, counterfactuals, attention-based methods, and more.
- **WHAT TO EXTRACT:** The taxonomy of XAI methods (local vs. global; post-hoc vs. intrinsic; model-agnostic vs. model-specific); the properties of good explanations (completeness, correctness, consistency, confidence, context); the comparison table of methods.
- **ACCESS:** https://arxiv.org/abs/1910.10045

---

### 3.6 ★★ Counterfactual Explanations for Image Classification — Visual Domain
**"Explainable Image Classification with Evidence Counterfactual"**
Vermeire, Brughmans, Goethals et al. — *Pattern Analysis and Applications*, 2022

- **WHY:** Extends the DiCE concept to image classification — finding which parts of an image, if removed, would change the predicted class. This is directly relevant to applying counterfactual reasoning to wafer map images rather than just tabular process data.
- **WHAT TO EXTRACT:** How counterfactual reasoning differs for images vs. tabular data; the evidence-based framing (what evidence is present that caused this classification); how this relates to your joint image+process counterfactual.
- **ACCESS:** https://link.springer.com/article/10.1007/s10044-021-01055-y

---

### 3.7 ★★ XAI Applied to Manufacturing
**"Explainable AI in Manufacturing and Industrial Cyber-Physical Systems: A Survey"**
*Electronics*, 2024

- **WHY:** Surveys ALL applications of XAI in manufacturing — fault detection, quality prediction, anomaly detection, and specifically semiconductor manufacturing. This paper validates your use case and shows what methods others have used in your domain.
- **WHAT TO EXTRACT:** How SHAP and LIME are used in semiconductor yield analysis; the specific examples of SHAP values identifying which process step contributed to yield loss; the limitations of post-hoc XAI in manufacturing settings.
- **ACCESS:** https://www.mdpi.com/2079-9292/13/17/3497

---

### 3.8 ★★ XAI for Root Cause Analysis — Zero-Defect Manufacturing
**"A Systematic Review on Machine Learning Methods for Root Cause Analysis Towards Zero-Defect Manufacturing"**
*Frontiers in Manufacturing Technology*, 2022

- **WHY:** Reviews how ML and XAI are combined specifically for root cause analysis in manufacturing — precisely what your project does. This paper identifies open research gaps that your project fills.
- **WHAT TO EXTRACT:** The taxonomy of RCA methods (statistical, ML, causal, knowledge-based); why explainability is critical for engineer trust in automated RCA; the specific gap: lack of counterfactual RCA in manufacturing.
- **ACCESS:** https://www.frontiersin.org/journals/manufacturing-technology/articles/10.3389/fmtec.2022.972712

---

## PILLAR 4 — Multi-Agent Systems
*Papers for designing your 4-agent architecture.*

---

### 4.1 ★★★ SemiFA — The Closest Paper to Your Project
**"SemiFA: An Agentic Multi-Modal Framework for Autonomous Semiconductor Failure Analysis Report Generation"**
*arXiv*, 2025

- **WHY:** This paper combines multi-agent AI with semiconductor defect analysis — it is the closest published work to your innovation. Study this carefully: understand what it does, what it cannot do, and where YOUR project goes further (counterfactual reasoning, IoT process correlation, agent debate protocol).
- **WHAT TO EXTRACT:** The agent architecture; how they handle multi-modal inputs (image + text); the failure analysis report format; the evaluation methodology; WHY they do NOT do counterfactual reasoning (the gap your project fills).
- **ACCESS:** https://arxiv.org/abs/2604.13236

---

### 4.2 ★★★ RCAgent — Multi-Agent Root Cause Analysis (Cloud Systems)
**"RCAgent: Cloud Root Cause Analysis by Autonomous Agents with Tool-Augmented Large Language Models"**
*CIKM*, 2024

- **WHY:** The first major paper showing multi-agent systems doing autonomous root cause analysis. Although it's about cloud systems (not semiconductors), the architecture directly maps to yours: multiple specialized agents, tool augmentation, coordinator agent, structured evidence synthesis.
- **WHAT TO EXTRACT:** The agent role decomposition; the tool-augmented reasoning pattern (agents can call analysis tools); the coordinator's evidence aggregation logic; the evaluation metrics for RCA quality (precision of root cause identification).
- **ACCESS:** https://arxiv.org/pdf/2310.16340

---

### 4.3 ★★★ ReAct — The Foundation of How Your Agents Think
**"ReAct: Synergizing Reasoning and Acting in Language Models"**
Yao, Zhao, Yu, Du, Shafran, Narasimhan, Cao — *ICLR*, 2023

- **WHY:** ReAct (Reason + Act) is the foundational architecture for how each of your 4 agents operates: think → decide what tool to call → call tool → observe result → think again. Every modern agentic system uses this pattern.
- **WHAT TO EXTRACT:** The Thought-Action-Observation loop; how ReAct differs from pure reasoning (Chain-of-Thought) and pure acting; the tool-calling mechanism; performance on multi-step reasoning tasks.
- **ACCESS:** https://arxiv.org/abs/2210.03629

---

### 4.4 ★★ Multi-Agent LLM Survey (IJCAI 2024)
**"Large Language Model based Multi-Agents: A Survey of Progress and Challenges"**
*IJCAI*, 2024

- **WHY:** The most cited survey of LLM-based multi-agent architectures. Covers coordinator patterns, communication protocols, memory mechanisms, and agent role specialization — all directly relevant to designing your Vision Agent, Process Agent, Counterfactual Agent, and Coordinator.
- **WHAT TO EXTRACT:** The taxonomy of multi-agent communication patterns (centralized vs. decentralized); the coordinator-worker pattern (your architecture); memory types for agents (short-term, long-term, episodic); how agents handle conflicting information.
- **ACCESS:** https://arxiv.org/abs/2402.01680

---

### 4.5 ★★ LLM-Based Agents for Fault Diagnosis
**"Exploring LLM-Based Agentic Frameworks for Fault Diagnosis"**
*PHM Society Annual Conference*, 2025

- **WHY:** Applies agentic AI (LLM agents) to industrial fault diagnosis from raw sensor data. Closely matches your Process Correlation Agent's role. The paper emphasizes that LLM agents produce inherently explainable outputs through natural language reasoning.
- **WHAT TO EXTRACT:** How sensor data is fed to an LLM agent; the diagnosis workflow; the explainability mechanism; limitations when sensor data is very high-dimensional.
- **ACCESS:** https://papers.phmsociety.org/index.php/phmconf/article/view/4350

---

### 4.6 ★★ Autonomous LLM Agents for Predictive Maintenance
**"Toward Autonomous LLM-Based AI Agents for Predictive Maintenance: State of the Art, Challenges, and Future Perspectives"**
*Applied Sciences*, 2025

- **WHY:** Reviews the entire landscape of LLM-based agentic systems for industrial maintenance and fault diagnosis. Gives you the vocabulary and framing to position your project in the broader context of industrial AI agents.
- **WHAT TO EXTRACT:** The distinction between information agents, decision-support agents, and fully autonomous agents; the governance and safety challenges for autonomous industrial agents; near-term vs. long-term adoption barriers.
- **ACCESS:** https://www.mdpi.com/2076-3417/15/21/11515

---

## PILLAR 5 — IoT, Sensor Streams & Process Parameter Correlation
*Papers for your IoT simulator design and Process Correlation Agent.*

---

### 5.1 ★★★ Semiconductor FDC — Fault Detection and Classification
**"Semiconductor Fault Detection and Classification for Yield Enhancement and Manufacturing Intelligence"**
Chien & Hsu — *Flexible Services and Manufacturing Journal*, 2012

- **WHY:** This paper establishes the FDC framework that your Process Correlation Agent automates. It uses multivariate process data (like your 6 IoT parameters) to detect and classify faults. This is what industry does today — your project explains WHY the fault happened.
- **WHAT TO EXTRACT:** The multi-way PCA approach for detecting process excursions across many parameters; the data mining rules for fault classification; how FDC data is structured in a real fab (SVID → FDC parameters transformation).
- **ACCESS:** https://link.springer.com/article/10.1007/s10696-012-9161-4

---

### 5.2 ★★★ Multivariate FDC with Deep Learning
**"Application of 1D ResNet for Multivariate Fault Detection on Semiconductor Manufacturing Equipment"**
*Sensors (MDPI)*, 2023

- **WHY:** Directly uses a 1D ResNet (same family as your backbone) on semiconductor sensor time-series data for fault detection. This validates your approach of combining deep learning with process sensor data.
- **WHAT TO EXTRACT:** How multivariate sensor streams are preprocessed (windowing, normalization); the 1D ResNet architecture for time-series; the class imbalance problem in real FDC data; comparison with traditional SPC thresholds.
- **ACCESS:** https://doi.org/10.3390/s23229099

---

### 5.3 ★★★ SECOM Dataset — IoT Simulator Calibration Reference
**"SECOM Dataset"**
McCann & Johnston — *UCI Machine Learning Repository*, 2008

- **WHY:** This is the dataset you use to calibrate your IoT simulator. Understanding the SECOM data structure — 591 features, 1567 samples, 14:1 class imbalance, 58% missing data — tells you what realistic semiconductor sensor data looks like.
- **WHAT TO EXTRACT:** The feature structure (which features correspond to which process steps); the missing value pattern (which sensors fail more often); the class imbalance ratio; the baseline model performance table.
- **ACCESS:** https://archive.ics.uci.edu/ml/datasets/SECOM

---

### 5.4 ★★ Explainable AutoML for Semiconductor Yield (SECOM Application)
**"Explainable AutoML (xAutoML) with Adaptive Modeling for Yield Enhancement in Semiconductor Smart Manufacturing"**
*arXiv*, 2024

- **WHY:** Uses SECOM data with XAI (SHAP) to find which of the 590 process parameters most affect yield. Directly shows how to apply XAI to your IoT parameter space. Your Process Correlation Agent does a simpler version of exactly this.
- **WHAT TO EXTRACT:** How SHAP values are computed for tabular sensor features; which features (process steps) were found most impactful in SECOM; the preprocessing pipeline for high-dimensional sensor data with missing values.
- **ACCESS:** https://arxiv.org/abs/2403.12381

---

### 5.5 ★★ Big Data Analytics for FDC — Multivariate IEEE Paper
**"Big Data Analytic for Multivariate Fault Detection and Classification in Semiconductor Manufacturing"**
*IEEE*, 2017

- **WHY:** Introduces LASSO + PCA for identifying which process parameters are the root cause of faults across hundreds of sensor readings. This is the statistical foundation your Process Correlation Agent is based on.
- **WHAT TO EXTRACT:** The LASSO feature selection approach for reducing 591 parameters to the key drivers; the 2-phase analysis (detect excursion → identify cause); the FDC data format and how SVID maps to parameters.
- **ACCESS:** https://ieeexplore.ieee.org/document/8256190

---

### 5.6 ★★ Plasma Etching Process Parameters — Physical Understanding
**"Wafer-Level Etch Spatial Profiling for Process Monitoring from Time-Series with Time-LLM"**
*arXiv*, 2025

- **WHY:** Explains the direct relationship between etch chamber parameters (gas flow, RF power, chamber pressure, temperature) and spatial non-uniformity on the wafer surface. This is the physical causal model your Counterfactual Agent must embody.
- **WHAT TO EXTRACT:** The specific parameters that affect etch uniformity (Table of parameters vs. effects); how spatial profiles of etch rate correlate with spatial defect patterns; the time-series structure of in-situ sensor data.
- **ACCESS:** https://arxiv.org/abs/2603.23576

---

## PILLAR 6 — Causal Reasoning & Multimodal Fusion
*Papers for the theoretical grounding of joint image + process counterfactual reasoning.*

---

### 6.1 ★★★ Multimodal Fusion for Manufacturing — Direct Domain Relevance
**"Multi-Modal Sensor Fusion with Machine Learning for Data-Driven Process Monitoring for Additive Manufacturing"**
*ScienceDirect*, 2021

- **WHY:** Shows how image data and sensor data are fused in a manufacturing quality prediction context. Your project does this for semiconductors — vision (wafer map) + sensor (IoT parameters). This is your architectural reference for the fusion layer.
- **WHAT TO EXTRACT:** The fusion architecture (separate encoders → concatenation → joint prediction); how modality imbalance is handled; the accuracy improvement from fusion vs. single-modality models.
- **ACCESS:** https://www.sciencedirect.com/science/article/abs/pii/S2214860421005182

---

### 6.2 ★★★ Causal Inference — Why "Correlation is Not Causation" Matters for Your Agent
**"A Survey on Causal Inference"**
Yao, Chu, Li, Liu et al. — *ACM Transactions on Knowledge Discovery from Data*, 2021

- **WHY:** Your Coordinator Agent claims "process parameter X CAUSED defect Y." This is a causal claim, not just a correlation. This survey explains the difference and gives you the vocabulary to make such claims rigorously.
- **WHAT TO EXTRACT:** The difference between association, intervention, and counterfactual (Pearl's ladder of causation); the Potential Outcomes framework; why observational data (your SECOM-calibrated simulator) can support causal claims with careful design.
- **ACCESS:** https://arxiv.org/abs/2109.13461

---

### 6.3 ★★ Joint Counterfactual Over Image and Tabular Features
**"Contrastive Counterfactual Visual Explanations with Overdetermination"**
White, Ngan et al. — *Machine Learning* (Springer), 2023

- **WHY:** Proposes CLEAR Image, a method for generating counterfactual explanations jointly over image regions and associated features — the closest published work to your joint image+process counterfactual idea. It outperforms GradCAM and LIME by 27% on a medical imaging benchmark.
- **WHAT TO EXTRACT:** The "contrastive explanation" framing (explaining why X was classified as A and not B); how image regions and non-image features are jointly perturbed; the overdetermination concept (multiple equally valid explanations).
- **ACCESS:** https://link.springer.com/article/10.1007/s10994-023-06333-w

---

### 6.4 ★★ Attention-Based Root Cause Analysis for Semiconductor
**"Attention Mechanism-Based Root Cause Analysis for Semiconductor Yield Enhancement Considering the Order of Manufacturing Processes"**
Lee, Choi et al. — *IEEE Transactions on Semiconductor Manufacturing*, 2022

- **WHY:** Directly addresses root cause identification for semiconductor yield using attention mechanisms over sequential process data. This is the most relevant published ML-based RCA paper in the semiconductor domain.
- **WHAT TO EXTRACT:** How process step ordering is incorporated into the model; the attention weights as a proxy for process step importance; comparison with SHAP-based attribution; the evaluation methodology for RCA quality.
- **ACCESS:** Search "Lee Choi 2022 attention root cause semiconductor yield IEEE TSM" — DOI: 10.1109/TSM.2022.3161027

---

## PILLAR 7 — Evaluation Methodology & Ablation Study Design
*Papers that show you HOW to evaluate your system rigorously.*

---

### 7.1 ★★★ Evaluation of XAI Methods — Metrics and Benchmarks
**"Quantitative Evaluation of Explanation Methods for Deep Learning"** (multiple authors, NeurIPS workshops)
Also: **"Sanity Checks for Saliency Maps"** — Adebayo et al., *NeurIPS 2018*

- **WHY:** You need to quantitatively evaluate your GradCAM++ heatmaps, not just show them visually. These papers establish metrics like Pointing Game accuracy, Average Drop, and Average Increase in Confidence.
- **WHAT TO EXTRACT:** The Average Drop metric (does the model become less confident when you mask the highlighted region?); the Sanity Check methodology (do saliency maps reflect model behavior or just input statistics?).
- **ACCESS:** https://arxiv.org/abs/1810.03292 (Sanity Checks paper)

---

### 7.2 ★★ Ablation Study Design for Multi-Module Systems
**"Flow-of-Action: SOP Enhanced LLM-Based Multi-Agent System for Root Cause Analysis"**
*WWW Industry Track*, 2025

- **WHY:** Shows how to design an ablation study for a multi-agent RCA system: remove one agent at a time, measure performance drop. This is exactly how you should compare "single-model (CNN only)" vs. "CNN + GradCAM" vs. "full multi-agent system."
- **WHAT TO EXTRACT:** The ablation table structure; which components contributed most to RCA accuracy; the evaluation protocol for comparing multi-agent vs. single-model baselines.
- **ACCESS:** Search "Flow-of-Action SOP LLM Multi-Agent Root Cause WWW 2025"

---

### 7.3 ★★ Counterfactual Validity Evaluation
**"Algorithmic Recourse: From Counterfactual Explanations to Interventions"**
Karimi, Schölkopf, Valera — *ACM FAccT*, 2021

- **WHY:** Defines how to evaluate whether counterfactual explanations are valid (actionable, feasible, and physically meaningful). Your counterfactuals must pass these checks — "Reduce gas flow by 200 sccm" is useless if the minimum physically possible is 300 sccm.
- **WHAT TO EXTRACT:** The distinction between counterfactual explanations (what to change) and algorithmic recourse (what to do); the feasibility constraint; the causal vs. non-causal counterfactual distinction; evaluation metrics: validity rate, proximity, sparsity.
- **ACCESS:** https://arxiv.org/abs/2002.06278

---

## Summary Reference Table

| # | Paper | Authors | Venue | Year | Pillar | Priority |
|---|-------|---------|-------|------|--------|----------|
| 1 | WM-811K Dataset | Wu, Jang, Chen | IEEE TSM | 2015 | 1 | ★★★ |
| 2 | Defect-Process Map (Geometric CNN) | Shin et al. | Scientific Reports | 2023 | 1 | ★★★ |
| 3 | Spatial Signature Analysis | Chen & Liu | Expert Sys. Appl. | 2000 | 1 | ★★★ |
| 4 | Defect Taxonomy | — | Adv. Eng. Informatics | 2024 | 1 | ★★ |
| 5 | Mixed-Type Defects (MixedWM38) | — | IEEE TCAD | 2023 | 1 | ★★ |
| 6 | Wafer Defect Review | — | J. Intell. Manuf. | 2026 | 1 | ★★ |
| 7 | ResNet | He et al. | CVPR | 2016 | 2 | ★★★ |
| 8 | GradCAM | Selvaraju et al. | ICCV/IJCV | 2017 | 2 | ★★★ |
| 9 | GradCAM++ | Chattopadhyay et al. | WACV | 2018 | 2 | ★★★ |
| 10 | Transfer Learning for Wafer | Imoto et al. | IEEE TSM | 2019 | 2 | ★★ |
| 11 | CNN + XAI on Wafer Maps | — | ResearchGate | 2025 | 2 | ★★ |
| 12 | LIME on Wafer Maps | Lee et al. | Micromachines | 2025 | 2 | ★★ |
| 13 | DiCE | Mothilal, Sharma, Tan | ACM FAccT | 2020 | 3 | ★★★ |
| 14 | Counterfactual Theory | Wachter et al. | Harvard J. L&T | 2017 | 3 | ★★★ |
| 15 | SHAP | Lundberg & Lee | NeurIPS | 2017 | 3 | ★★★ |
| 16 | LIME | Ribeiro et al. | KDD | 2016 | 3 | ★★★ |
| 17 | XAI Survey | Arrieta et al. | Information Fusion | 2020 | 3 | ★★★ |
| 18 | Counterfactual Image XAI | Vermeire et al. | Pattern Anal. Appl. | 2022 | 3 | ★★ |
| 19 | XAI in Manufacturing Survey | — | Electronics | 2024 | 3 | ★★ |
| 20 | XAI for RCA in Manufacturing | — | Frontiers | 2022 | 3 | ★★ |
| 21 | SemiFA (Multi-agent + Semiconductor) | — | arXiv | 2025 | 4 | ★★★ |
| 22 | RCAgent | Wang et al. | CIKM | 2024 | 4 | ★★★ |
| 23 | ReAct | Yao et al. | ICLR | 2023 | 4 | ★★★ |
| 24 | Multi-Agent Survey | — | IJCAI | 2024 | 4 | ★★ |
| 25 | LLM Agents for Fault Diagnosis | — | PHM Society | 2025 | 4 | ★★ |
| 26 | Autonomous LLM for Pred. Maint. | — | Appl. Sciences | 2025 | 4 | ★★ |
| 27 | Semiconductor FDC | Chien & Hsu | Flex. Serv. Manuf. | 2012 | 5 | ★★★ |
| 28 | 1D ResNet for FDC | Tchatchoua et al. | Sensors MDPI | 2023 | 5 | ★★★ |
| 29 | SECOM Dataset | McCann & Johnston | UCI | 2008 | 5 | ★★★ |
| 30 | xAutoML on SECOM | — | arXiv | 2024 | 5 | ★★ |
| 31 | Multivariate FDC Big Data | — | IEEE | 2017 | 5 | ★★ |
| 32 | Plasma Etch + IoT Sensor | — | arXiv | 2025 | 5 | ★★ |
| 33 | Multimodal Fusion (Mfg) | — | ScienceDirect | 2021 | 6 | ★★★ |
| 34 | Causal Inference Survey | Yao et al. | ACM TKDD | 2021 | 6 | ★★★ |
| 35 | Contrastive Counterfactual Image | White et al. | Machine Learning | 2023 | 6 | ★★ |
| 36 | Attention-Based RCA Semiconductor | Lee, Choi et al. | IEEE TSM | 2022 | 6 | ★★ |
| 37 | Sanity Checks for Saliency Maps | Adebayo et al. | NeurIPS | 2018 | 7 | ★★★ |
| 38 | Algorithmic Recourse | Karimi et al. | ACM FAccT | 2021 | 7 | ★★ |

---

## Reading Priority Order (8 Weeks)

**Week 1:** Papers 1, 2, 3 (Pillar 1 core — understand your dataset and domain)
**Week 2:** Papers 7, 8, 9 (Pillar 2 core — ResNet, GradCAM, GradCAM++)
**Week 3:** Papers 13, 14, 15 (Pillar 3 core — DiCE, Counterfactual theory, SHAP)
**Week 4:** Papers 16, 17, 18 (Pillar 3 remaining — LIME, XAI survey, image counterfactuals)
**Week 5:** Papers 21, 22, 23 (Pillar 4 core — SemiFA, RCAgent, ReAct)
**Week 6:** Papers 27, 28, 29, 32 (Pillar 5 — FDC, IoT, SECOM, etch parameters)
**Week 7:** Papers 33, 34, 36 (Pillar 6 — multimodal fusion, causality, RCA for semiconductor)
**Week 8:** Papers 37, 38, 4, 5, 6 (Pillar 7 — evaluation; remaining Pillar 1 context)

---
