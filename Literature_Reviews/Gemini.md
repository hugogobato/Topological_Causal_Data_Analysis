# Toward **[Topological Causal Data Analysis](https://arxiv.org/abs/2603.02289)**: a literature review at the intersection of **[Causal Inference](https://ieeexplore.ieee.org/ielx7/5/9420072/09363924.pdf)** and **[Topological Data Analysis](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)**

My overall read is that your proposed domain is **plausible and timely**, but it should be framed as a **new umbrella research program** rather than as a claim that “nobody has connected causality and topology before.” The literature already contains several partially overlapping strands: topology used as a learning-theoretic language for causal identifiability, topology/geometry used for causal discovery in dynamical systems, TDA used to define causal effects on non-Euclidean outcomes, and TDA used as a regularizer for robust treatment-effect estimation. What is still missing is a **unified field definition, common estimands, shared assumptions, benchmark tasks, and a coherent theory of identification/inference** across these strands. That gap is exactly where “Topological Causal Data Analysis” can be positioned. [Source](https://proceedings.neurips.cc/paper/2021/file/2c463dfdde588f3bfc60d53118c10d6b-Paper.pdf), [Source](https://arxiv.org/pdf/2603.02289), [Source](https://openreview.net/pdf?id=YIhzCp1XKv), [Source](https://arxiv.org/pdf/1605.02570)

## A compact map of the current literature

| Literature strand | What topology is doing | Representative papers | Why it matters for TCDA |
|---|---|---|---|
| Theoretical topology of causation | Topology formalizes learnability/verifiability of causal claims | Ibeling & Icard (2021) | Shows topology can say something fundamental about causal inference, though this is **not TDA proper** |
| Dynamical/topological causality | Geometry/topology of reconstructed state spaces is used to infer directed influence | Harnack et al. (2016); Bando, Kaji & Yaguchi (2022) | Suggests causal direction can be encoded in shape/manifold distortion |
| Topological treatment effects | Persistent-homology summaries define causal estimands for complex outcomes | Kim & Lee (2026); Saki & Faghihi (2026) | Most direct precursor to a TCDA outcome-based framework |
| Topology-aware causal representation learning | TDA regularizes latent representations for robust effect estimation | Farzam et al. (2025) | Suggests topology can be a **causal inductive bias**, not just an outcome descriptor |
| Geometry/interventions in latent causal learning | Interventions reveal identifiable geometric structure in latent spaces | Schölkopf et al. (2021); Ahuja et al. (2023) | Not TDA-specific, but gives the strongest bridge to identifiability theory |
| Statistical inference for TDA on networks/time series | Bootstrap/simulation/testing for topological summaries | El-Yaagoubi, Chung & Ombao (2023); Iniesta et al. (2022) | Important because TCDA will fail without uncertainty quantification |

Sources: [Ibeling & Icard 2021](https://proceedings.neurips.cc/paper/2021/file/2c463dfdde588f3bfc60d53118c10d6b-Paper.pdf), [Kim & Lee 2026](https://arxiv.org/pdf/2603.02289), [Farzam et al. 2025](https://openreview.net/pdf?id=YIhzCp1XKv), [Harnack et al. 2016](https://arxiv.org/pdf/1605.02570), [Schölkopf et al. 2021](https://ieeexplore.ieee.org/ielx7/5/9420072/09363924.pdf), [Ahuja et al. 2023](https://proceedings.mlr.press/v202/ahuja23a/ahuja23a.pdf), [El-Yaagoubi et al. 2023](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2023.1293504/pdf), [Iniesta et al. 2022](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)

## 1. **[Topology in causal inference theory](https://proceedings.neurips.cc/paper/2021/file/2c463dfdde588f3bfc60d53118c10d6b-Paper.pdf)** is real, but it is not yet **[Topological Data Analysis](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)**

A useful starting point is Ibeling and Icard’s “A topological perspective on causal inference.” Their contribution is conceptually important because it proves that certain causal inferences require assumptions that are statistically unverifiable, using topology on spaces of structural causal models. But this paper uses topology in a **learning-theoretic/philosophical** sense—weak topologies on model spaces—not in the modern TDA sense of persistence diagrams, Mapper, filtrations, or topological summaries of data clouds. For your paper, this is valuable because it lets you say: topology is already present in causal theory, but **data-analytic topology** has not yet been systematized as a causal methodology. [Source](https://proceedings.neurips.cc/paper/2021/file/2c463dfdde588f3bfc60d53118c10d6b-Paper.pdf)

## 2. **[Topological causality in dynamical systems](https://arxiv.org/pdf/1605.02570)** is an early bridge

Harnack et al.’s “On Causality in Dynamical Systems” is one of the clearest early bridge papers. It studies directed effective influence in coupled nonlinear systems via reconstructed manifolds and local mappings between them. This is not persistent homology either, but it is very close in spirit to TCDA because the key causal signal lives in **shape, reconstruction geometry, and deformation of state-space structure** rather than in classical regression coefficients or conditional independences alone. It is especially relevant if you want TCDA to include time series, attractors, nonlinear systems, neuroscience, or climate/ecology applications. [Source](https://arxiv.org/pdf/1605.02570)

A more direct TDA-facing example appears in the 2022 paper “Causal inference for empirical dynamical systems based on persistent homology,” which indicates that persistent homology can be applied to reconstructed attractors for causal inference in correlated systems. Even though this line is still small, it is important because it shows that persistent-homology-based causal reasoning is not just hypothetical—it already exists in at least embryonic form within dynamical-systems research. [Source](https://www.jstage.jst.go.jp/article/jsiaml/14/0/14_69/_pdf)

## 3. **[Topological causal effects](https://arxiv.org/pdf/2603.02289)** are the clearest current intersection

The most direct intersection I found is Kim and Lee’s 2026 preprint “Topological Causal Effects.” This paper explicitly defines treatment effects through changes in topological summaries of complex outcomes, using persistence-based silhouettes to create a functional estimand, the Topological Average Treatment Effect. That is a major conceptual step because it moves causality beyond mean shifts in Euclidean spaces and treats topology itself as the scientifically salient object that interventions may alter—for example, in molecules, medical images, connectivity data, or other non-Euclidean outcomes. If you are writing a TCDA manifesto paper, this is probably the single most important paper to discuss carefully. [Source](https://arxiv.org/pdf/2603.02289)

At the same time, this literature is still emerging. The paper itself acknowledges limitations: it focuses on macroscopic structural change, relies on computationally intensive persistent homology, and is currently framed around relatively standard causal settings before extensions to continuous treatments, instrumental variables, and longitudinal exposures. That means the literature has begun to define topological estimands, but it has not yet built a mature general theory of identification, robustness, or design. [Source](https://arxiv.org/pdf/2603.02289)

A closely related 2026 follow-up, “Beyond Means: Topological Causal Effects under Persistent-Homology Ignorability,” suggests that this line is already expanding toward more classical estimands like ATE/CATE but with topology-sensitive assumptions. That is another sign that the field is starting to cohere, though it remains pre-paradigmatic. [Source](https://arxiv.org/pdf/2603.14169)

## 4. **[Topology-aware treatment effect estimation](https://openreview.net/pdf?id=YIhzCp1XKv)** shows topology can be a causal inductive bias

Another strong precursor is Farzam et al.’s 2025 work on topology-aware robust representation balancing. Their framework regularizes causal representation learning by minimizing discrepancies between persistence diagrams of treated and control representations. The important idea is not merely “use TDA features”; it is that topological structure can stabilize representation learning under heavy-tailed noise and improve counterfactual estimation. This pushes topology from being an outcome descriptor to being a **regularizer and prior** inside the causal learning pipeline. [Source](https://openreview.net/pdf?id=YIhzCp1XKv)

For your proposed TCDA domain, this is important because it suggests at least four roles for topology: as **outcome**, as **covariate geometry**, as **latent representation prior**, and as **dynamical signature**. A field definition that explicitly unifies those four roles would already be a genuine contribution, because the existing literature treats them as separate problems. [Source](https://openreview.net/pdf?id=YIhzCp1XKv), [Source](https://arxiv.org/pdf/2603.02289), [Source](https://arxiv.org/pdf/1605.02570)

## 5. **[Causal representation learning](https://ieeexplore.ieee.org/ielx7/5/9420072/09363924.pdf)** supplies the identifiability agenda TCDA will need

The broader causal representation learning literature is not usually phrased in TDA language, but it is indispensable for a serious TCDA agenda. Schölkopf et al.’s “Toward causal representation learning” argues that causal variables often need to be discovered from high-dimensional observations and that identification is impossible without extra structure, such as interventions, distribution shifts, or inductive biases like independent causal mechanisms. This matters because TCDA will face exactly the same issue: **a persistence diagram or Mapper graph is not automatically a causal variable**. You need assumptions explaining when topological structure is causally meaningful rather than merely descriptive. [Source](https://ieeexplore.ieee.org/ielx7/5/9420072/09363924.pdf)

Ahuja et al.’s “Interventional causal representation learning” is especially relevant because it shows how interventions create geometric signatures that enable latent identifiability. Even though the paper uses support geometry rather than persistent homology, it provides a model for how TCDA could move from “interesting topological summaries” to “identifiable topological latent factors under interventions.” In other words, the path to a rigorous TCDA probably goes through the same triangle of **interventions, geometry, and identifiability**. [Source](https://proceedings.mlr.press/v202/ahuja23a/ahuja23a.pdf)

## 6. **[Topological Data Analysis](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)** already has the tools TCDA needs, but not the causal theory

The TDA review by Iniesta et al. is useful because it summarizes why TDA is attractive in applied science: it can detect structure in high-dimensional data, identify subpopulations, remain stable under perturbations, and provide interpretable summaries of shape via persistence or Mapper. Those strengths are exactly what causal inference often lacks when treatment effects or latent heterogeneity are structural rather than linear or Euclidean. So, from the TDA side, the toolbox is already mature enough to be useful. [Source](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)

But the same review also flags the weaknesses that TCDA must take seriously: parameter sensitivity in Mapper, uncertainty about significance testing, bootstrap validity gaps for some topological summaries, and the danger of overinterpreting persistent features without good inferential calibration. So a causal paper that simply “plugs in TDA” without addressing inference and design will look incomplete. [Source](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)

The same point is reinforced by the NeurIPS 2022 analysis of persistent homology’s effectiveness, which argues that persistent homology can be genuinely informative but is highly sensitive to pipeline choices and should not be sold as a universal solution. For a TCDA paper, this is a good cautionary citation: topology is powerful, but only when the filtration, summary, and scientific question match each other. [Source](https://proceedings.neurips.cc/paper_files/paper/2022/file/e637029c42aa593850eeebf46616444d-Paper-Conference.pdf)

## 7. **[Statistical inference for topological summaries](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2023.1293504/pdf)** is still underdeveloped, and that is a major opening

El-Yaagoubi, Chung, and Ombao’s 2023 paper on dependence networks in TDA is highly relevant because it focuses on simulation-based statistical inference and hypothesis testing for topological summaries in multivariate time series. That is exactly the kind of machinery TCDA will need if it wants to say not only that treated and control groups “look topologically different,” but that they differ with quantified uncertainty under a formal causal design. Right now, the inferential side of the intersection is much less mature than the feature-engineering side. [Source](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2023.1293504/pdf)

This inferential immaturity may be one of your paper’s best selling points. A field called TCDA can be justified not merely by saying “causality and TDA intersect,” but by showing that the existing intersection lacks shared answers to the hardest questions: what is the estimand, when is it identified, how do we estimate it, how do we test it, and how do we interpret it scientifically? [Source](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2023.1293504/pdf), [Source](https://arxiv.org/pdf/2603.02289), [Source](https://openreview.net/pdf?id=YIhzCp1XKv)

---

## What is still missing — and therefore what your paper can claim

A strong framing sentence for your paper would be something like this:

> Existing work connects causality and topology in **isolated ways**—through topological learnability theory, dynamical-systems geometry, persistence-based causal estimands, and topology-aware representation learning—but there is not yet a unified research program that treats topological structure as a first-class object in causal design, identification, estimation, and inference.

That claim is well supported by the literature above. There are precursors, but there is still no commonly recognized field with shared scope, standard tasks, benchmark suites, or a mature theory connecting TDA summaries to potential outcomes, structural causal models, counterfactuals, and intervention design. [Source](https://proceedings.neurips.cc/paper/2021/file/2c463dfdde588f3bfc60d53118c10d6b-Paper.pdf), [Source](https://arxiv.org/pdf/2603.02289), [Source](https://openreview.net/pdf?id=YIhzCp1XKv), [Source](https://ieeexplore.ieee.org/ielx7/5/9420072/09363924.pdf)

## A workable definition of **[Topological Causal Data Analysis](https://arxiv.org/pdf/2603.02289)**

You could define **Topological Causal Data Analysis (TCDA)** as:

> the study of how topological structure in observed, latent, or outcome spaces can be used to formulate, identify, estimate, and interpret causal effects.

That definition is broad enough to include four subareas:  
first, **topology as outcome**, where treatment changes persistent structure;  
second, **topology as representation**, where topological constraints regularize causal learning;  
third, **topology as dynamical evidence**, where causal direction is inferred from reconstructed state-space geometry;  
and fourth, **topology as heterogeneity map**, where Mapper-like summaries reveal effect-modifying subpopulations or latent regimes. [Source](https://arxiv.org/pdf/2603.02289), [Source](https://openreview.net/pdf?id=YIhzCp1XKv), [Source](https://arxiv.org/pdf/1605.02570), [Source](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)

## The most promising open problems and research questions

### **1. What is a causal estimand when the scientific signal is topological?**
Classical causal inference gives you ATE, CATE, mediation effects, path-specific effects, and so on. TCDA needs analogues for persistence diagrams, barcodes, landscapes, silhouettes, Mapper graphs, and possibly Euler characteristic curves. Kim and Lee make an important start, but the space of possible topological estimands is still barely explored. [Source](https://arxiv.org/pdf/2603.02289)

### **2. When are topological summaries causally identifiable rather than merely predictive?**
A persistence diagram may summarize shape, but what assumptions make it a valid causal variable? This is the key identifiability question. The causal representation literature suggests that interventions, distribution shifts, and modularity assumptions are likely necessary. A TCDA theory should explain when topological summaries preserve the causal information needed for effect estimation and when they destroy it. [Source](https://ieeexplore.ieee.org/ielx7/5/9420072/09363924.pdf), [Source](https://proceedings.mlr.press/v202/ahuja23a/ahuja23a.pdf)

### **3. How should confounding be handled when covariates or outcomes are non-Euclidean and topological?**
Most causal pipelines assume tabular covariates or vector embeddings. TCDA needs methods for confounding adjustment when units are graphs, point clouds, images, manifolds, or persistence objects. This includes propensity scores or balancing scores defined on topological summaries, as well as robustness analyses for topological mismatch between treated and control groups. [Source](https://openreview.net/pdf?id=YIhzCp1XKv), [Source](https://arxiv.org/pdf/2603.02289)

### **4. Can topological heterogeneity reveal effect modifiers or latent causal subpopulations?**
Mapper and related TDA tools are good at discovering subgroups and trajectories. A major open question is whether those topological strata correspond to **causal effect modifiers**, not just descriptive clusters. This is an especially promising angle for precision medicine, neuroimaging, and longitudinal patient-state spaces. [Source](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)

### **5. How should TCDA deal with time-varying treatment and nonlinear dynamics?**
The dynamical-systems literature suggests that causal information may appear in manifold deformation, attractor geometry, or persistence over delay reconstructions. But TCDA still lacks a unified treatment of interventions, feedback, recurrence, and topological summaries for temporal causal discovery. This looks like one of the richest open areas. [Source](https://arxiv.org/pdf/1605.02570), [Source](https://www.jstage.jst.go.jp/article/jsiaml/14/0/14_69/_pdf), [Source](https://dl.acm.org/doi/pdf/10.1145/3705297)

### **6. What are the right inferential procedures and null models?**
If a treatment changes topology, how do we quantify uncertainty? Bootstrap methods, permutation methods, simulation-based nulls, and asymptotic theory all exist in pieces within TDA, but causal inference places extra demands because assignment mechanisms and ignorability assumptions matter. TCDA needs design-aware topological inference, not just generic significance testing. [Source](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2023.1293504/pdf), [Source](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)

### **7. Which topological summaries are scientifically interpretable enough for causal explanation?**
Persistent homology is mathematically elegant, but scientists often need explanations in domain language: lesions, loops in vessel structure, connectivity holes, molecular folding motifs, subpopulation branches, regime transitions. A TCDA agenda should include interpretability layers that map abstract topological changes back to domain-relevant mechanisms. [Source](https://arxiv.org/pdf/2603.02289), [Source](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf)

### **8. How do we benchmark TCDA methods?**
The literature repeatedly notes the absence of ground truth and proper simulation frameworks for topological inference on time series and networks. TCDA will need benchmark suites where the treatment mechanism, causal graph, and topological signal are all known. Without that, comparisons will remain anecdotal. [Source](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2023.1293504/pdf), [Source](https://dl.acm.org/doi/pdf/10.1145/3705297)

## The best way to position your paper

I would recommend that your paper **not** claim “we introduce the first connection between causal inference and TDA.” That claim would be too strong. A better and more defensible positioning is:

1. prior work has established **local bridges** between causality and topology;  
2. those bridges are fragmented across different communities;  
3. there is no unified field organizing them around common causal questions;  
4. your paper proposes **Topological Causal Data Analysis** as that organizing framework. [Source](https://arxiv.org/pdf/2603.02289), [Source](https://openreview.net/pdf?id=YIhzCp1XKv), [Source](https://arxiv.org/pdf/1605.02570), [Source](https://proceedings.neurips.cc/paper/2021/file/2c463dfdde588f3bfc60d53118c10d6b-Paper.pdf)

That framing is stronger intellectually anyway. It lets you write a paper that is simultaneously a literature review, field-defining perspective, and research agenda.

---

## Two especially useful figures from the literature

These are worth citing in your paper draft or talk because they visually capture the core idea of the field:

- **Treatment-induced changes in topological summaries** from *Topological Causal Effects* (Fig. 1 / Fig. 3): [view figure](https://arxiv.org/pdf/2603.02289#page=2) and [view application figure](https://arxiv.org/pdf/2603.02289#page=9)  
- **Geometric signatures of interventions in latent space** from *Interventional Causal Representation Learning* (Fig. 1): [view figure](https://proceedings.mlr.press/v202/ahuja23a/ahuja23a.pdf#page=1)  
- **Manifold-mapping view of directed influence** from *On Causality in Dynamical Systems* (Fig. 1): [view figure](https://arxiv.org/pdf/1605.02570#page=2)

## A short thesis statement you could use almost verbatim

> We propose **Topological Causal Data Analysis (TCDA)** as a new research domain for studying causal questions in which topological structure is not merely descriptive but causally meaningful—as an outcome of intervention, a representation prior, a marker of latent heterogeneity, or a signature of dynamical influence. While recent work has introduced topological causal effects, topology-aware effect estimation, and topological approaches to dynamical causality, these contributions remain fragmented. TCDA aims to unify them under a common program of causal design, identification, estimation, uncertainty quantification, and scientific interpretation. [Source](https://arxiv.org/pdf/2603.02289), [Source](https://openreview.net/pdf?id=YIhzCp1XKv), [Source](https://arxiv.org/pdf/1605.02570)

## Core references to anchor the paper

The most important references for your bibliography, in my view, are these:  
[Ibeling & Icard, 2021](https://proceedings.neurips.cc/paper/2021/file/2c463dfdde588f3bfc60d53118c10d6b-Paper.pdf),  
[Schölkopf et al., 2021](https://ieeexplore.ieee.org/ielx7/5/9420072/09363924.pdf),  
[Harnack et al., 2016](https://arxiv.org/pdf/1605.02570),  
[Bando, Kaji & Yaguchi, 2022](https://www.jstage.jst.go.jp/article/jsiaml/14/0/14_69/_pdf),  
[Iniesta et al., 2022](https://ddd.uab.cat/pub/sort/sort_a2022v46n1/sort_a2022v46n1p115.pdf),  
[El-Yaagoubi, Chung & Ombao, 2023](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2023.1293504/pdf),  
[Ahuja et al., 2023](https://proceedings.mlr.press/v202/ahuja23a/ahuja23a.pdf),  
[Farzam et al., 2025](https://openreview.net/pdf?id=YIhzCp1XKv),  
[Kim & Lee, 2026](https://arxiv.org/pdf/2603.02289),  
and likely also [Saki & Faghihi, 2026](https://arxiv.org/pdf/2603.14169).

If you want, I can next turn this into one of three paper-ready formats: a **formal related-work section**, an **annotated bibliography with summaries of 15–20 papers**, or a **2–3 page position-paper introduction** for your proposed “Topological Causal Data Analysis” paper.