Topological Causal Data Analysis: A Literature Review at the Intersection of Causal Inference and Topological Data Analysis
Overview
This literature review examines the intersection of Causal Inference (CI) and Topological Data Analysis (TDA), two methodological paradigms that have evolved largely independently until recent years. While CI provides a rigorous statistical framework for quantifying cause–effect relationships from observational data, TDA offers powerful tools for extracting and summarizing the latent geometric and topological structure of complex data. Their convergence—embodied in works explicitly invoking “topological causal inference”—points toward a rich new research domain that this review aims to chart as a foundation for proposing Topological Causal Data Analysis (TCDA) .

The review is organized into three main parts. Section 1 surveys core contributions that explicitly integrate topological concepts into causal inference workflows, covering causal discovery via topological ordering, TDA-enhanced causal effect estimation, theoretical topological perspectives on CI, and persistent homology for dynamical systems. Section 2 identifies open problems and gaps that define a research frontier at this intersection. Section 3 synthesizes the literature to outline a research trajectory, concluding with a structured bibliography.

1. Core Contributions and Intersections
1.1. Causal Discovery with Topological Ordering
The classical problem of learning Directed Acyclic Graphs (DAGs) from observational data can be reframed as first identifying a topological ordering of variables—a permutation such that all causal edges point from earlier to later positions—and then pruning spurious edges. A substantial body of recent work has explored this “topology-first” paradigm.

Tran et al. (2024) propose a framework that integrates topological ordering information directly into differentiable Bayesian structure learning to guarantee acyclicity of inferred graphs. Their approach demonstrates how explicit knowledge of variable ordering can constrain the optimization landscape, improving both consistency and computational efficiency.

Wu and Xie (2026) go further with Score-Schur Topological Sort (SSTS) , an algorithm that extracts topological order directly from unconstrained generative models, bypassing non‑convex acyclicity penalties entirely. The authors establish that “the causal hierarchy leaves a geometric signature within the score function: iterative graph marginalization is mathematically equivalent to computing the Schur complement of the Score‑Jacobian Information Matrix” under linear conditions. SSTS scales to nonlinear graphs with up to 
d
=
1000
d=1000 variables, reframing scalable causal discovery “from a constrained optimization problem to a statistical estimation challenge.”

Xu, Mameche, and Vreeken (2025) present TOPIC, an information‑theoretic framework for causal discovery in topological order based on Kolmogorov complexity. TOPIC is fully identifiable and extends to both i.i.d. and non‑i.i.d. continuous settings, frequently outperforming specialized methods on continuous, time‑series, and interventional data.

Other notable contributions in this thread include Barroso et al. (2024) , who propose a constraint‑based algorithm that automatically determines causal relevance thresholds—termed topological thresholds—to infer causal networks, thereby accelerating the inference of causal DAGs, as well as Hybrid Top‑Down Global Causal Discovery methods that leverage local causal substructures and introduce nonparametric constraint‑based pruning. Together, these works establish topological ordering as a core bridging concept between graph‑theoretic causal models and TDA’s emphasis on structural invariants.

1.2. Topological Data Analysis for Causal Effect Estimation
A distinct line of work uses TDA not for discovering causal structure but for estimating causal effects when outcomes are complex, non‑Euclidean, or noise‑corrupted.

Kim and Lee (2026) —in what is perhaps the most direct precursor to a “Topological Causal Data Analysis” paradigm—develop a framework that defines treatment effects through differences in the topological structure of potential outcomes, summarized by power‑weighted silhouette functions of persistence diagrams. They propose an efficient, doubly robust estimator in a fully nonparametric model, establish functional weak convergence, and construct a formal test for the null hypothesis of no topological effect. Empirical studies show reliable quantification of topological treatment effects “across diverse complex outcome types.” This work explicitly integrates TDA’s signature summary (persistence diagrams) into the Rubin causal model, offering a rigorous statistical foundation for outcome‑space topology.

Farzam et al. (2025) address robustness challenges in high‑dimensional representation learning for causal inference. Their Topology‑Aware Treatment Effect Estimation (TATEE) framework leverages TDA to enhance representation stability in neural networks. Theoretical analysis establishes conditions under which topological summaries improve robustness to input noise, particularly for heavy‑tailed distributions. Importantly, TATEE requires no ground‑truth or validation data, making it suitable for purely observational settings common in causal inference, and its overhead scales linearly with data size while remaining constant in input dimension.

1.3. Topological Perspective on Causal Inference Theory
A more abstract strand of research examines causal inference itself through a topological lens, asking what fundamental limitations and possibilities emerge when causal models are endowed with topological structure.

A 2024 contribution presents a topological learning‑theoretic perspective on causal inference by defining topologies on spaces of Structural Causal Models (SCMs). The authors prove a topological causal hierarchy theorem, showing that substantive, assumption‑free causal inference is possible only in a “meager set” of SCMs. Via a known correspondence between open sets in the weak topology and statistically verifiable hypotheses, their results imply that inductive assumptions sufficient to license valid causal inferences are statistically unverifiable in principle—a kind of “no‑free‑lunch” theorem for causality.

This work is complemented by conceptual essays that reframe causality as topological reconstruction. On such view, “causal inference uncovers a hidden topological structure that governs how variables influence each other. Every causal relation defines a partial order, inducing an Alexandrov topology like causal set theory in spacetime. Statistical identifiability becomes a question of separability: do two causal hypotheses occupy distinct topological regions?” In this framing, causal reasoning becomes “continuity + order in a stratified manifold space,” where distance encodes influence strength, order encodes direction, and topology encodes stability.

1.4. Persistent Homology for Causal Inference in Dynamical Systems
Persistent homology (PH)—TDA’s flagship method for quantifying multi‑scale topological features—has been applied to causal inference in empirical dynamical systems.

Bando, Kaji, and Yaguchi (2022) combine delay coordinate embedding with persistent homology to infer causality between pairs of scalar time series from possibly coupled deterministic dynamical systems. Their approach encodes the topology of reconstructed attractors via persistent homology and compares systems using a metric defined on persistence diagrams. As they note, standard PH tools are “confined to analyzing data through a single filter parameter,” but many scenarios require multiple parameters to attain finer insights—a limitation that points directly toward open problems (see Section 2.4).

In the neuroscience domain, the Causality‑Based Topological Ranking (CBTR) method integrates causal inference to assess effective brain connectivity with Hodge Decomposition to rank brain regions based on mutual influence, accurately identifying hierarchical structures in multivariate time‑series data. Similarly, Topological Hawkes Processes (THP) draw a connection between graph convolution in the topology domain and temporal convolution in time domains, enabling causal structure learning on event sequences. These domain‑specific applications illustrate how topological techniques can enrich causal analysis in high‑dimensional, time‑varying systems.

1.5. Additional Relevant Intersections
Other notable connections include:

Causal network topology analysis formalized as a methodology for characterizing causal context of risk events, articulating ontological concepts underpinning repeatable topology network analysis, and justifying the selection of network metrics for causal risk management.

Deep causal inference as manifold geometry, where “causality is not a fixed graph but an evolving geometric system” and “learning searches for topological invariants: boundaries of influence, loops of feedback, singularities of bifurcation”.

Topology‑informed causal attention in CausalNET, which unveils causal structures on event sequences using topology‑informed attention mechanisms.

The deep_causality_topology Rust crate, which provides rigorous topological data structures and algorithms for causal modeling, geometric deep learning, and complex systems analysis, bridging discrete data (graphs, point clouds) with causal reasoning.

2. Open Problems and Gaps
Despite significant progress, the integration of TDA and CI remains nascent. The following open problems define a frontier that Topological Causal Data Analysis (TCDA) could systematically address.

2.1. Generalization to Nonlinear and High‑Dimensional Systems
Most current work—including the influential persistent homology method of Bando et al.—assumes deterministic dynamical systems or linear structural equation models. Question: Can topological causal inference be extended to nonlinear, stochastic systems with latent confounding? Existing PH tools are “confined to analyzing data through a single filter parameter”, yet causal structures in complex systems are inherently multi‑scale and multi‑parameter. Multidimensional persistence (e.g., Effective Multidimensional Persistence (EMP) frameworks that integrate descriptor functions for graph classification) offers a promising path, but its integration with causal identification remains unexplored.

2.2. Statistical Inference and Uncertainty Quantification
While Kim and Lee establish functional weak convergence for their topological causal effect estimator, general uncertainty quantification for topology‑based causal claims is underdeveloped. Questions: What are the sampling distributions of topological summaries (persistence diagrams, landscapes, silhouettes) under causal interventions? How can one construct valid confidence intervals or hypothesis tests for topological causal parameters? The link between topology and statistical verifiability—touched upon in the topological causal hierarchy theorem—suggests fundamental limits that deserve deeper investigation.

2.3. Causality in Topological Representations
Most TDA methods operate on point clouds or graphs, while causal inference typically works with variables and structural equations. Question: How should one define “causal effect” directly on the space of persistence diagrams or other topological representations? Kim and Lee take an important step by summarizing persistence diagrams via silhouette functions, but more general notions of functional causal effects on topological spaces remain to be formalized. The conceptual framing of causality as “topological reconstruction from samples on an unseen causal surface” is evocative but lacks operational criteria for identifiability and estimation.

2.4. Scalability and Computational Challenges
Persistent homology computation scales poorly with data size and dimension, limiting its application to large‑scale causal problems. The TATEE framework achieves linear scaling in data size, and SSTS scales to 
d
=
1000
d=1000 variables, but these are still modest compared to modern high‑dimensional causal inference settings (e.g., genomics with tens of thousands of variables). Question: Can topological causal methods be approximated or subsampled while preserving theoretical guarantees? What role can topological deep learning (TDL) play in learning computationally efficient topology‑aware causal representations?

2.5. Domain‑Specific Applications and Validation
Several application areas are ripe for topological causal analysis but lack systematic methodology:

Medical imaging and computational pathology: TDA has demonstrated “15–20% improvements over traditional methods” for tumor characterization, cardiovascular imaging, and COVID‑19 detection, yet causal inference in these domains remains largely associational. Question: Can persistence images and landscapes be used to estimate causal effects of interventions (e.g., treatment regimens) on radiological outcomes?

Brain connectivity: Promises and pitfalls of TDA for brain connectivity analysis have been explored, but “effective connectivity graphs capturing direct causal interactions” remain underexploited. Question: How can directed persistence or persistent homology on directed graphs be leveraged for causal discovery in neural time series?

Spatial epidemiology: TDA frameworks for detecting structural voids in censored epidemiological data with “causal labelling” point toward new methods for distinguishing natural gaps from intervention effects.

2.6. Bridging TDA and Causal Representation Learning
Causal representation learning (CRL) aims to recover latent causal variables from entangled observations. Question: Can TDA’s ability to uncover latent manifold structure be combined with CRL’s identifiability guarantees? Recent work on “linear causal representation learning by topological ordering, pruning, and disentanglement” suggests a path, but nonlinear, nonparametric settings remain open.

3. Summary and Path Forward for Topological Causal Data Analysis
The literature reveals two principal modes of integrating topology and causality: (i) using topological ordering as a computational primitive for DAG learning, and (ii) using topological summaries (persistence diagrams, landscapes, silhouettes) as outcome representations for causal effect estimation. A third, more fundamental mode—treating causality itself as a topological property of data manifolds—remains largely programmatic.

Topological Causal Data Analysis (TCDA) , as a proposed research domain, would systematically unify these threads by addressing the open problems identified above. Specific research directions include:

Topological Causal Discovery: Develop algorithms that use multidimensional persistent homology to learn causal DAGs from multi‑scale, heterogeneous data without assuming linearity or determinism.

Topological Causal Estimation: Extend the Kim–Lee framework to handle time‑varying treatments, mediation, and interference, with rigorous uncertainty quantification.

Foundational Theory: Formalize the relationship between topological invariants (e.g., Betti numbers, persistent homology groups) and causal identifiability, building on the topological causal hierarchy theorem.

Computational Infrastructure: Build scalable TDA‑for‑causality toolkits integrating state‑of‑the‑art persistent homology libraries (e.g., GUDHI) with causal inference engines.

Domain Translation: Validate TCDA methods in high‑stakes applications such as personalized medicine (imaging genomics), neuroscience (effective connectivity), and public health (spatial intervention evaluation).

The convergence of TDA and CI is timely and fertile. By framing causal questions topologically and topological questions causally, TCDA promises new theoretical insights, more robust estimators, and novel applications at the frontier of data science.

Bibliography
Bando, H., Kaji, S., & Yaguchi, T. (2022). Causal inference for empirical dynamical systems based on persistent homology. JSIAM Letters, 14, 69–72.

Farzam, A., Aloui, A., Tarokh, V., & Sapiro, G. (2025). Topology-aware robust representation balancing for estimating causal effects. *NeurIPS 2025 High-dimensional Learning Dynamics Workshop*.

Kim, K., & Lee, H. (2026). Topological causal effects. ICLR 2026. arXiv:2603.02289.

Wu, R., & Xie, H. (2026). Optimization-free topological sort for causal discovery via the Schur complement of score Jacobians. arXiv:2604.25295.

Tran, Q.-D., Nguyen, P., Duong, B., & Nguyen, T. (2024). Constraining acyclicity of differentiable Bayesian structure learning with topological ordering. Knowledge and Information Systems, 66, 5605–5630.

Xu, S., Mameche, S., & Vreeken, J. (2025). Information-theoretic causal discovery in topological order. AISTATS 2025.

Barroso, F., Gomes, D., & Baxter, G. J. (2024). Inference of causal networks using a topological threshold. arXiv:2404.14460.

AITopics. (2024). A topological perspective on causal inference. Conference Proceedings.

Ma, M. (2025). Causal inference as topological reconstruction in deep manifolds. LinkedIn post.

Promises and pitfalls of Topological Data Analysis for brain connectivity analysis. (2021). bioRxiv.

Unraveling the Invisible: Topological Data Analysis as the New Frontier in Radiology’s Diagnostic Arsenal. (2025). PMC.

THPs: Topological Hawkes Processes for Learning Causal Structure on Event Sequences. (2022). IEEE Explore.

Deep_causality_topology Rust crate. (2026). lib.rs.

Causal network topology analysis: Characterizing causal context for risk management. (2024). Wiley Online Library.

Hybrid Top-Down Global Causal Discovery with Local Search for Linear and Nonlinear Additive Noise Models. (2024). Semantic Scholar.

Topological Analysis of Seizure-Induced Changes in Brain Hierarchy Through Effective Connectivity. (2024). arXiv.

TDA Engine v2.1: A Computational Framework for Detecting Structural Voids in Spatially Censored Epidemiological Data. (2026). medRxiv.

Survey and Evaluation of Causal Discovery Methods for Time Series. (2024). *IJCAI-23*.

