<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Perform a literature review regarding Causal Inference and Topological Data Analysis (like their current and possible intersection/ open problems/questions) so that I can use for a paper I will write proposing a novel research domain called Topological Causal Data Analysis

Here is a concise literature review and positioning map for a paper proposing **Topological Causal Data Analysis**. The strongest current story is that causal inference and TDA already share a concern with robust structure under noise and high dimensionality, but they have mostly evolved separately; the emerging opportunity is to use topological summaries as causal targets, effect modifiers, diagnostics, and representation tools.[^1][^2][^3]

## 1) Why these fields are converging

Causal inference asks what changes when we intervene, while TDA asks what structure persists across scales; both care about features that are stable under perturbation, but they formalize “signal” differently. In practice, causal inference is increasingly used in settings with networks, high-dimensional covariates, latent structure, and nonstandard dependence, which makes geometric and topological summaries attractive as auxiliary representations or assumptions-checking tools. TDA, meanwhile, has expanded beyond persistent homology into Laplacians, sheaf methods, and related spectral/topological constructions, suggesting a broader toolkit for causal problems than just Betti-number summaries.[^4][^5][^6][^2][^1]

## 2) What exists today

A few papers already hint at the intersection. One line uses topology inside modeling pipelines, such as CWGCNA, which combines network structure and causal mediation ideas in omics analysis, showing that topological structure can be useful in causal biological workflows. Another line uses TDA for dynamical or flow data and then applies observational causal reasoning to parts of the system, as in topological flow data analysis for transient flow patterns. A more explicit causal-TDA contribution is a 2026 paper on topological causal effects, which defines persistent-homology-based causal estimands and a “persistent-homology ignorability” condition, showing that mean-based causal effects can miss pure topology changes in outcome distributions.[^7][^8][^3]

## 3) Main conceptual gap

The central gap is that standard causal estimands are scalar or vector-valued summaries of averages, while TDA produces objects such as persistence diagrams, landscapes, barcodes, Laplacians, or filtrations that are not naturally handled by classical causal estimators. A second gap is identification: persistent homology generally does not commute with mixing over covariates, so marginal topological effects are not automatically identified from conditional assumptions. A third gap is inference: even when a topological causal estimand is defined, one still needs valid uncertainty quantification, robustness to sampling variability, and practical estimators that scale to real data.[^3][^1]

## 4) Promising intersection themes

The clearest research opportunities are these:

- Topological causal estimands: define causal effects not just on means, but on distributional shape, connectivity, holes, and multiscale geometry.[^3]
- Topology as covariate representation: use persistence features or topological embeddings as sufficient or near-sufficient summaries for nuisance adjustment, heterogeneity discovery, or representation learning.[^6][^1]
- Causal discovery with topology: use topological signatures to constrain graph search, detect latent confounding, or identify regime changes in causal graphs, especially in networked and dynamical systems.[^5][^8][^4]
- Topology-aware interventions: study how interventions reshape persistence diagrams or topological invariants, especially in scientific systems where structure itself is the outcome.[^3]
- Multi-scale causal structure: pair filtration scale with time, exposure dose, or spatial scale to build causal models that vary across resolutions.[^2][^1]


## 5) Open problems

For a paper proposing “Topological Causal Data Analysis,” the most defensible open problems are:

1. Identification theory for topological estimands under realistic confounding, selection, and interference.
2. A causal analogue of stability theorems: when do small perturbations in data imply small perturbations in causal topological effects?
3. Estimation and inference for diagram-valued or functional causal effects with valid confidence sets.
4. Topological adjustment under post-treatment bias and collider structure.
5. Causal discovery from topological summaries, especially in time series, manifolds, networks, and point clouds.
6. Handling mixtures and heterogeneity, since topological features can disappear or appear after averaging across subpopulations.[^3]
7. Choosing the right topological representation for a causal question: persistence diagrams, landscapes, Laplacians, sheaves, or geometric invariants.[^1]

## 6) Positioning your paper

A strong framing is to say that **Topological Causal Data Analysis** is not just “using topology for causal inference,” but a program with three layers: topological representation, causal identification, and causal inference on topological objects. That lets you distinguish your proposal from general TDA-in-ML papers and from standard causal ML papers, while aligning it with the emerging literature on topology beyond persistent homology. You can present the field as a response to cases where causal effects are invisible to mean-based summaries but visible in the shape of the outcome law, especially in multimodal, networked, or dynamical data.[^8][^4][^1][^3]

## 7) Suggested research questions

Good paper-level questions include:

- When is a topological summary causally sufficient for adjustment or mediation?
- Can persistence diagrams be used as causal outcomes, mediators, or effect modifiers?
- How do interventions alter homological features across scales?
- What are the identification assumptions for topology-valued potential outcomes?
- Can topological invariants improve causal discovery in high-dimensional or networked systems?
- How do we estimate and test topological treatment effects with finite-sample guarantees?[^4][^1][^3]


## 8) Reading map

For your literature review, I would organize references into four clusters:

- Foundations of TDA and broader topological methods: the 2025 review on TDA and topological deep learning beyond persistent homology.[^1]
- TDA applications and inference: classic and applied TDA surveys and hypothesis-testing papers.[^9][^10][^2]
- Causal inference in complex dependence settings: network interference, high-dimensional time series, and causal representation learning.[^5][^6][^4]
- Direct causal-topological work: the 2026 topological causal effects paper and related causal-network/topological biology work.[^7][^3]

A concise thesis sentence for your paper could be: **Topological Causal Data Analysis seeks causal estimands, identification strategies, and inference procedures whose targets are topological summaries of distributions, dynamical systems, and networks, rather than only scalar averages**.[^1][^3]
<span style="display:none">[^11][^12][^13][^14][^15][^16][^17][^18][^19][^20][^21][^22]</span>

<div align="center">⁂</div>

[^1]: https://link.springer.com/10.1007/s10462-025-11462-w

[^2]: https://www.tandfonline.com/doi/full/10.1080/13658816.2022.2155654

[^3]: https://www.semanticscholar.org/paper/111393a069a8cef66994ce796029f6146b9693f5

[^4]: https://www.semanticscholar.org/paper/ea9867ecf151eade547f39e8addeb44fac4c4592

[^5]: https://gmssrj.com/index.php/main/article/view/133

[^6]: https://arxiv.org/abs/2509.22553

[^7]: https://academic.oup.com/nargab/article/doi/10.1093/nargab/lqae042/7658051

[^8]: https://www.semanticscholar.org/paper/fd664ccb7558fb3eddfdcca79cf321b7795f7914

[^9]: https://wseas.com/journals/mathematics/2023/a065106-1711.pdf

[^10]: https://linkinghub.elsevier.com/retrieve/pii/S1110256X17300433

[^11]: https://dl.acm.org/doi/10.1145/3789297.3789353

[^12]: https://etamaths.com/index.php/ijaa/article/view/4605

[^13]: https://annalsmcs.org/index.php/amcs/article/view/494

[^14]: https://pubs.acs.org/doi/10.1021/acs.jcim.5c02266

[^15]: https://www.semanticscholar.org/paper/ca8f33c96baa34bc1989d838f3add1ce3e437dc8

[^16]: https://pubs.acs.org/doi/10.1021/acs.jcim.4c02111

[^17]: https://www.semanticscholar.org/paper/03648b1c53fa1ee3f08974f88ad8312bc12276bb

[^18]: https://ijamjournal.org/ijam/publication/index.php/ijam/article/view/1296

[^19]: https://www.semanticscholar.org/paper/0830e8efb002f29c9b584796562cf400d41773b4

[^20]: https://linkinghub.elsevier.com/retrieve/pii/S0020740325005788

[^21]: https://www.semanticscholar.org/paper/21e113a7c4782dd7bdf3572fe89072d70c25c9c1

[^22]: https://academic.oup.com/tse/article/doi/10.1093/tse/tdaf015/8019779

