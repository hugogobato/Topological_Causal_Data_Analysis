# From Persistent Homology to Topos Models: A Comprehensive Literature Review on the Intersection of Causal Inference and Topological Data Analysis

**Abstract.** This review systematically examines the emerging convergence between **causal inference (CI)** and **topological data analysis (TDA)**, two fields that have historically developed along largely independent trajectories. While causal inference provides rigorous frameworks for quantifying intervention effects and discovering causal structure from observational data, topological data analysis offers powerful tools for characterizing the shape, connectivity, and multiscale organization of complex data. We identify six primary modes of intersection between these disciplines: (1) the use of **persistent homology** to define topology-aware causal estimands for non-Euclidean outcomes; (2) **Hodge decomposition** methods for causal ranking and the identification of feedback cycles in directed networks; (3) **sheaf-theoretic and topos-theoretic frameworks** that generalize Pearl's do-calculus using higher-order category theory; (4) **higher-order categorical approaches** employing simplicial objects and quasicategories to unify causal inference with reinforcement learning; (5) **topological ordering algorithms** that exploit the DAG structure for scalable causal discovery; and (6) **Mapper-based approaches** that leverage TDA for causal feature selection and subgroup discovery. Our analysis reveals that this intersection, which we term **Topological Causal Data Analysis (TCDA)**, is poised to address fundamental limitations in both parent fields. We catalog applications spanning neuroscience, genomics, precision medicine, and financial systems, identify critical open problems including the non-commutativity of persistent homology with covariate mixtures, the computational intractability of sheaf-based causal discovery at scale, and the need for principled topological identifiability conditions, and propose a research agenda for establishing TCDA as a distinct methodological discipline.

---

## 1. Executive Summary and Taxonomy

The intersection of causal inference and topological data analysis represents one of the most promising yet underexplored frontiers in modern statistical methodology. Causal inference, grounded in the potential outcomes framework of Neyman and Rubin and the structural causal model (SCM) framework of Pearl, provides a rigorous mathematical language for reasoning about interventions, counterfactuals, and cause-effect relationships. Topological data analysis, rooted in algebraic topology and computational geometry, offers a complementary toolkit for characterizing the shape, connectivity, and multiscale organization of data. While these fields have developed largely independently, recent work suggests that their convergence, which we refer to as **Topological Causal Data Analysis (TCDA)**, could address fundamental limitations in both disciplines.

The motivation for TCDA arises from a critical gap in current methodology. Standard causal estimands, such as the **average treatment effect (ATE)** and the **conditional average treatment effect (CATE)**, target changes in the expected value of outcomes under alternative interventions. These estimands are fundamentally scalar summaries that can miss intervention-induced changes in the shape, geometry, or topological structure of outcome distributions. A canonical failure mode occurs when control outcomes are unimodal, treated outcomes become bimodal, and both distributions share the same mean. In such cases, the ATE is identically zero even though the geometry and topology of the outcome law have changed substantially. This limitation is not merely academic; it arises naturally in biomedical settings where treatments can alter macromolecular conformations, in neuroscience where stimuli reshape brain connectivity patterns, and in materials science where processing conditions modify microstructural topology.

Simultaneously, topological data analysis has largely operated in a descriptive or predictive mode, extracting features from complex data for downstream machine learning tasks. The integration of causal reasoning into TDA pipelines remains in its infancy, with most applications treating topological summaries as opaque feature vectors rather than as estimands with formal causal interpretations. This review documents the state of this emerging intersection and charts a course toward its maturation as a distinct methodological discipline.

| Category | Representative Works | Key Contribution | Mathematical Core |
|---|---|---|---|
| Persistent Homology + Causal Estimands | Kim & Lee (ICLR 2025); Saki & Faghihi (2026) | Define causal effects via topological summaries; prove identifiability under topological ignorability | Power-weighted silhouette functions; Wasserstein stability; doubly robust estimation |
| Hodge Decomposition + Causal Ranking | El-Yaagoubi et al. (2024); NOCURL (Jiang et al.) | Decompose edge flows into gradient (causal), curl (feedback), and harmonic (global cycle) components | Combinatorial Hodge theory; Hodge Laplacian on simplicial complexes |
| Sheaf/Topos-Theoretic Causal Models | Mahadevan (NeurIPS 2025); HOLOGRAPH (Kim, 2025) | Generalize do-calculus using subobject classifiers; formalize causal discovery as sheaf cohomology | Topos theory; Lawvere-Tierney topology; presheaf descent |
| Higher-Order Category Theory + Causality | Mahadevan (2022; 2023); Universal Causality | Unify CI and RL using simplicial objects; model interventions as face operators | Quasicategories; Kan complexes; nerve of a category |
| Topological Ordering for Causal Discovery | TOPIC (Xu et al., AISTATS 2025); SCORE (Rolland et al.) | Exploit DAG acyclicity via topological sorts; score-based leaf node identification | Topological sort of DAGs; Hessian of log-likelihood; score matching |
| Mapper + Causal Feature Discovery | DataRefiner TDA; TDA for manufacturing | Use Mapper networks to identify topologically important features for causal models | Mapper algorithm; Reeb graphs; topological network visualization |
| Topological Event Sequences | S2GCSL (Li et al., NeurIPS 2024); CausalNET | Model causal propagation over topological network structures | Hawkes processes on graphs; Granger causality with network topology |
| Causal Emergence + Topology | Krasnovsky (2025); Hoel et al. (2013) | Quantify when macro-level causal models outperform micro-level descriptions using topological aggregation | Effective information; coarse-graining; causal emergence |

The organization of this review reflects the taxonomy above. Following this summary, we provide self-contained primers on the foundations of causal inference and topological data analysis, respectively. We then examine each mode of intersection in depth, catalog applications, enumerate open problems, and propose a research agenda for the formalization of Topological Causal Data Analysis.

---

## 2. Foundations of Causal Inference

Understanding the intersection of causal inference with topology requires a firm grasp of the foundational frameworks that underpin modern CI. We review the three dominant paradigms: the **potential outcomes framework**, the **structural causal model framework**, and the **graphical model approach** to causal discovery.

### 2.1 The Potential Outcomes Framework

The potential outcomes framework, often called the **Neyman-Rubin causal model**, conceptualizes causal effects as comparisons between counterfactual outcomes. For a binary treatment variable $A \in \{0, 1\}$ and an outcome $Y$, each unit $i$ is assumed to have two potential outcomes: $Y_i(1)$, the outcome under treatment, and $Y_i(0)$, the outcome under control. The **individual treatment effect** is $\tau_i = Y_i(1) - Y_i(0)$, but this quantity is fundamentally unidentified because we observe at most one potential outcome for each unit. This is the **fundamental problem of causal inference**.

Identification is typically achieved through the assumption of **strong ignorability** (or **unconfoundedness**): $(Y(1), Y(0)) \perp\!\!\!\perp A \mid X$, where $X$ is a vector of observed covariates. Under this assumption, the **average treatment effect** $\tau = \mathbb{E}[Y(1) - Y(0)]$ is identified by $\mathbb{E}_X[\mathbb{E}[Y \mid A=1, X] - \mathbb{E}[Y \mid A=0, X]]$. The **conditional average treatment effect** $\tau(x) = \mathbb{E}[Y(1) - Y(0) \mid X=x]$ allows for treatment effect heterogeneity. Estimation strategies include regression adjustment, propensity score weighting, and doubly robust methods that combine outcome modeling with propensity score modeling to achieve $\sqrt{n}$-consistency and semiparametric efficiency.

A critical limitation of this framework, as we discuss later, is its reliance on **Euclidean summaries**. The ATE and CATE are scalar quantities that capture shifts in the first moment of the outcome distribution but are entirely insensitive to changes in shape, modality, or topological structure. When outcomes are graphs, images, point clouds, or probability distributions, scalar summaries may be scientifically inadequate. This limitation has motivated the development of topology-aware causal estimands.

### 2.2 Structural Causal Models and the Do-Calculus

Pearl's **structural causal model (SCM)** framework provides an alternative but mathematically equivalent foundation. An SCM $M = \langle U, V, F, P(U) \rangle$ consists of a set of exogenous variables $U$, a set of endogenous variables $V$, a set of structural functions $F = \{f_i\}$ that determine each $V_i \in V$ as a function of its parents and exogenous noise, and a distribution $P(U)$ over the exogenous variables. The structural equations $V_i = f_i(Pa(V_i), U_i)$ induce a **directed acyclic graph (DAG)** $G$ over the variables in $V$.

The power of the SCM framework lies in its capacity to formalize interventions. The **do-operator**, $do(V_i = v)$, represents an external intervention that sets variable $V_i$ to value $v$, overriding its natural structural equation. Pearl developed the **do-calculus**, a set of three inference rules that permit the transformation of expressions involving the do-operator into expressions involving only observational (conditional) probabilities. The do-calculus is **complete**: if a causal effect is identifiable from the observational distribution and the causal graph, then there exists a sequence of do-calculus rules that yields the identification formula.

Key identification strategies include the **back-door criterion**, which specifies a set of variables that blocks all confounding paths between treatment and outcome, and the **front-door criterion**, which exploits mediators for identification when confounders are unobserved. For more complex settings, **generalized adjustment criteria** and **causal identification algorithms** such as those implemented in the `causaleffect` R package provide automated procedures for determining identifiability and deriving identification formulas from arbitrary DAGs.

### 2.3 Causal Discovery from Observational Data

When the causal graph is unknown, it must be inferred from data. **Causal discovery** (or **structure learning**) algorithms fall into three main categories. **Constraint-based methods**, such as the **PC algorithm** and its variants, use conditional independence tests to identify the **Markov equivalence class** of DAGs that are consistent with the observed independence structure. Because multiple DAGs can encode the same set of conditional independences, constraint-based methods typically return a **completed partially directed acyclic graph (CPDAG)** or a **partial ancestral graph (PAG)** when latent confounders may be present.

**Score-based methods**, such as the **Greedy Equivalence Search (GES)** algorithm, search over the space of DAGs or equivalence classes, optimizing a scoring function that balances model fit with complexity. Recent work has developed continuous optimization formulations, notably **NOTEARS** and its extensions, which reformulate the acyclicity constraint as a continuous differentiable penalty $h(W) = \text{tr}(e^{W \circ W}) - d$, enabling gradient-based optimization over the space of weighted adjacency matrices. This approach and its successors, including **DAGMA** and methods based on the **log-determinant acyclicity characterization**, have dramatically expanded the scalability of score-based causal discovery.

**Functional causal model-based methods** exploit additional assumptions about the data-generating process to identify causal directions beyond what is possible from conditional independence alone. The **linear non-Gaussian acyclic model (LiNGAM)** assumes linear relationships with non-Gaussian noise and uses independent component analysis to identify the causal order. **Additive noise models (ANMs)** assume that the effect can be expressed as a function of the cause plus independent noise, and test for this independence in both directions. These methods can identify the full DAG rather than just its Markov equivalence class, but they rely on assumptions that may not hold in practice.

### 2.4 Causal Representation Learning

**Causal representation learning** aims to discover latent causal variables and their relationships from high-dimensional, unstructured observations. In the **latent causal model** framework, observed variables $X$ are generated from latent causal variables $Z$ through a mixing function $X = g(Z)$, where $Z$ follows a structural causal model. The goal is to recover both the latent variables $Z$ and their causal structure. Recent work has established **identifiability results** showing that under certain conditions, including access to interventional data or appropriate distributional assumptions on the latent noise, both the latent variables and the causal graph can be recovered up to acceptable ambiguities. The **CREATOR** algorithm and related methods use topological ordering, pruning, and disentanglement to achieve this recovery, demonstrating the natural connection between causal ordering and topological structure even in this foundational causal inference setting.

---

## 3. Foundations of Topological Data Analysis

Topological data analysis provides a family of techniques for characterizing the shape of data using tools from algebraic topology. Unlike geometric methods that depend on precise distances and coordinates, topological methods are **invariant under continuous deformations**, making them robust to noise and coordinate choices. We review the core concepts necessary for understanding the CI-TDA intersection.

### 3.1 Simplicial Complexes and Homology

The fundamental building blocks of TDA are **simplicial complexes**. A $k$-simplex is the convex hull of $k+1$ affinely independent points: a 0-simplex is a vertex, a 1-simplex is an edge, a 2-simplex is a triangle, and so on. A **simplicial complex** is a collection of simplices that is closed under taking faces: if a simplex is in the complex, then all of its faces are also in the complex. Simplicial complexes generalize graphs to higher-dimensional relationships and provide a combinatorial representation of topological spaces.

**Simplicial homology** is an algebraic procedure for counting topological features of a simplicial complex. The $k$-th **Betti number** $\beta_k$ counts the number of $k$-dimensional holes: $\beta_0$ counts connected components, $\beta_1$ counts one-dimensional loops (cycles), $\beta_2$ counts two-dimensional voids, and so on. Homology groups $H_k$ provide more refined information, encoding not just the number of holes but their algebraic structure. These invariants are robust under continuous deformations and can be computed efficiently using linear algebra over the simplicial complex.

### 3.2 Persistent Homology and Persistence Diagrams

While simplicial homology characterizes a single topological space, **persistent homology** tracks how topological features evolve as a space is constructed at varying scales. Given a **filtration**, a nested sequence of simplicial complexes $\emptyset = K_0 \subseteq K_1 \subseteq \cdots \subseteq K_n = K$, persistent homology records when each topological feature (connected component, loop, void) appears (is **born**) and when it disappears (is **killed**) as the filtration parameter increases.

The output of persistent homology is a **persistence diagram**, a multiset of points $(b, d)$ in the upper half-plane $\mathbb{R}^2_{b<d}$, where each point represents a topological feature born at scale $b$ and dying at scale $d$. The **persistence** (or **lifetime**) of a feature is $d - b$. Features with long persistence are considered "real" topological signals, while features with short persistence are typically attributed to noise. The **Wasserstein distance** and **bottleneck distance** provide metrics on the space of persistence diagrams, and **stability theorems** guarantee that small perturbations to the input data result in small perturbations to the persistence diagrams.

Practical computation of persistent homology typically proceeds by constructing a filtration from data. Common approaches include the **Vietoris-Rips filtration**, which connects points within a given distance threshold, and the **Cech filtration**, which uses intersecting balls. Software packages such as `Ripser`, `GUDHI`, and `Dionysus` provide efficient implementations.

### 3.3 Mapper and Topological Summaries

The **Mapper algorithm**, introduced by Singh, Memoli, and Carlsson, provides an alternative approach to TDA that produces a combinatorial summary of data in the form of a graph. Mapper takes as input a point cloud dataset, a **filter function** (or lens) $f: X \to \mathbb{R}^d$ that maps the data to a lower-dimensional space, and a clustering algorithm. It constructs a graph where nodes correspond to clusters of data points within overlapping level sets of the filter function, and edges connect nodes that share data points. The resulting **Mapper graph** provides a topological skeleton of the data that can reveal loops, branches, and flares corresponding to meaningful structures.

Mapper has found wide application in domains where interpretable summaries are essential, including genomics, neuroscience, and materials science. Unlike persistent homology, which produces algebraic invariants, Mapper produces a visualizable network that can be directly interpreted by domain scientists. Variants such as the **Kilimanjaro Mapper** and **Ball Mapper** have been developed to address parameter selection challenges and computational scalability.

### 3.4 Hodge Theory and Combinatorial Laplacians

**Hodge theory** provides a deep connection between topology, geometry, and analysis on simplicial complexes. The **Hodge decomposition theorem** states that any vector field (or more generally, any $k$-cochain) on a simplicial complex can be uniquely decomposed into three orthogonal components: a **gradient** (or **cocurl**) component, a **curl** (or **coboundary**) component, and a **harmonic** component. Formally, for a 1-cochain (edge flow) $X$ on a simplicial complex:

$$X = X_G + X_C + X_H$$

where $X_G \in \text{im}(\delta_0)$ is a gradient flow derived from a scalar potential on vertices (modeling direct causal propagation), $X_C \in \text{im}(\delta_1^\top)$ is a curl flow derived from a vector potential on triangles (modeling local feedback cycles), and $X_H \in \ker(\mathcal{L}_1)$ is a harmonic flow that captures global cyclic structures over non-contractible loops.

The **Hodge Laplacian** $\mathcal{L}_1 = \delta_0^\top \delta_0 + \delta_1 \delta_1^\top$ generalizes the graph Laplacian to higher-dimensional structures and provides a spectral framework for analyzing flows on simplicial complexes. Hodge decomposition has emerged as a powerful tool for causal inference on networks because it naturally separates directional (gradient) from cyclic (curl, harmonic) flow components, providing a topological decomposition of causal influence.

### 3.5 Sheaves and Cosheaves over Simplicial Complexes

A **sheaf** on a topological space assigns data (vector spaces, sets, or other algebraic structures) to open sets in a manner that respects restriction maps and satisfies **gluing axioms**. Sheaves formalize the idea of **local data that can be patched together to form global data**. On a simplicial complex, a **cellular sheaf** assigns vector spaces to simplices and linear maps to face relations. Sheaf cohomology measures the obstruction to constructing global sections from local data and provides topological invariants that generalize simplicial cohomology.

**Cosheaves** are the dual notion, with extension maps rather than restriction maps, and are particularly natural for modeling data that propagates forward rather than backward. Sheaf-theoretic methods have recently been applied to network science, opinion dynamics, and distributed optimization. In the context of causal inference, sheaves provide a mathematical framework for formalizing how local causal beliefs about subsets of variables can be combined into globally consistent causal models, as we discuss in the sheaf-theoretic causal discovery section.

---

## 4. The Intersection: Topological Causal Data Analysis

We now turn to the core contribution of this review: a systematic examination of the six primary modes through which causal inference and topological data analysis have begun to intersect. Each subsection traces the intellectual history, formalizes the key mathematical ideas, identifies the most important contributions, and highlights open questions.

### 4.1 Persistent Homology for Causal Effect Estimation

The most direct intersection of CI and TDA concerns the definition and estimation of causal effects for **non-Euclidean outcomes** using persistent homology. Traditional causal estimands target changes in expected outcomes, but many scientific questions concern changes in the **shape, structure, or topology** of outcomes. This section examines the foundational papers that have established this subfield.

#### 4.1.1 Motivation: When Scalar Estimands Fail

The limitations of scalar causal estimands are most starkly illustrated by a canonical example. Suppose a treatment induces a change in the outcome distribution from unimodal to bimodal, while preserving the mean. In this case, the ATE is identically zero, even though the treatment has fundamentally altered the geometry and topology of the outcome. This is not a contrived scenario: in precision medicine, a drug may create a subpopulation of responders and non-responders, producing a bimodal outcome distribution. In materials science, processing conditions may induce phase transitions that alter microstructural topology. In neuroscience, stimuli may create or destroy loops in neural population activity patterns. A causal framework that targets only the mean misses these scientifically salient effects entirely.

Kim and Lee formalize this problem in their **Topological Causal Effects** paper (presented at ICLR 2025), arguing that "as modern scientific outcomes become increasingly complex, standard causal estimands and methods that rely on Euclidean summaries can fail to detect meaningful intervention-induced changes in the underlying structure of the outcome." They propose a class of causal estimands that quantify intervention-induced changes in the topological structure of complex outcomes, summarized by **power-weighted silhouette functions** of persistence diagrams.

#### 4.1.2 Defining Topological Causal Estimands

The central challenge in defining topological causal estimands is that persistent homology does not commute with mixtures. Given a mixture distribution $P = \sum_i w_i P_i$, the persistence diagram of $P$ is not generally a mixture of the persistence diagrams of the $P_i$. This non-linearity complicates the definition of marginal estimands, because the potential outcome distributions $P(Y(1))$ and $P(Y(0))$ are themselves marginal distributions over covariates.

Kim and Lee address this challenge by defining their estimands in terms of **conditional topological effects**. Let $\phi_k(\cdot)$ denote the power-weighted silhouette function for $k$-dimensional persistent homology. The **topological causal effect** is defined as:

$$\tau_\phi(a, a') = \mathbb{E}_X[\phi(D_k(Y(a) \mid X)) - \phi(D_k(Y(a') \mid X))]$$

where $D_k(\cdot)$ denotes the $k$-dimensional persistence diagram of a sample from the conditional outcome distribution. This definition conditions on covariates $X$, computes the topological contrast at each covariate value, and averages over the covariate distribution. This approach avoids the commutativity problem by applying persistent homology to conditional distributions rather than marginal distributions.

Independently, Saki and Faghihi develop a closely related framework in their paper **"Beyond Means: Topological Causal Effects under Persistent-Homology Ignorability"** (arXiv 2026). They formalize a **persistent-homology ignorability condition**, define **topological analogues of CATE and ATE**, and prove identifiability results. Their framework clarifies that "a marginal persistence-diagram effect is not identified from conditional topological ignorability alone because persistent homology does not in general commute with mixtures over covariates." They place the mathematically sound conditional estimands at the center of their theory while retaining the marginal effect as a motivating quantity.

#### 4.1.3 Doubly Robust Estimation and Inference

The practical estimation of topological causal effects presents significant challenges because both the outcome model (for computing persistence diagrams from conditional distributions) and the propensity score model must be estimated nonparametrically. Kim and Lee develop an **efficient, doubly robust, fully nonparametric estimator** that achieves $\sqrt{n}$ rates under a standard product-rate condition on nuisance errors. Their estimator combines an estimated outcome model (which predicts the topological summary under treatment) with an estimated propensity score model in a manner analogous to the Augmented Inverse Probability Weighting (AIPW) estimator for scalar outcomes.

The key technical contributions include: (1) **stability bounds** for weighted silhouettes under Wasserstein perturbations of persistence diagrams, which ensure that small estimation errors in the outcome model translate into small errors in the causal estimand; (2) a **functional weak convergence** result that enables the construction of valid confidence bands for the topological causal effect function; and (3) a **formal hypothesis test** of the null hypothesis of no topological effect with asymptotically valid size and consistency. These theoretical results place topological causal inference on the same rigorous footing as classical semiparametric causal inference.

Empirical studies in both papers demonstrate that the proposed methods reliably quantify topological treatment effects across diverse complex outcome types, including molecular graphs, brain networks, and dynamical systems. A synthetic experiment with mean-preserving topology change shows that mean-based causal estimands remain near zero while the proposed topological effect increases sharply and remains recoverable after adjustment for confounding.

#### 4.1.4 Open Questions in Topological Causal Inference

Despite these advances, several important questions remain. First, the **choice of filter function** and **scale parameters** in persistent homology introduces analyst degrees of freedom that may affect the interpretability and stability of topological causal effects. Second, the **computational cost** of computing persistence diagrams for large samples of complex outcomes remains a practical barrier. Third, **alternative topological summaries** beyond silhouettes, such as persistence landscapes, persistence images, and Betti curves, have yet to be fully explored as causal estimands. Fourth, the extension to **continuous treatments**, **time-varying treatments**, and **network interference** settings remains largely open.

### 4.2 Hodge Decomposition for Causal Ranking and Cycle Detection

While persistent homology characterizes the topology of point cloud data, **Hodge theory** provides tools for analyzing directed networks and flows. The application of Hodge decomposition to causal inference focuses on separating acyclic causal propagation from cyclic feedback structures in network data.

#### 4.2.1 The Hodge Decomposition of Edge Flows

Given a directed network with edge flows (e.g., Granger causal influences, information transfer estimates, or regulatory interactions), the Hodge decomposition separates the flow into three orthogonal components. The **gradient component** $X_G$ represents flows that can be explained by a potential function on nodes, modeling hierarchical causal propagation from upstream to downstream variables. The **curl component** $X_C$ represents local cyclic flows around triangles of nodes, modeling feedback loops among tightly connected variables. The **harmonic component** $X_H$ represents global cyclic flows that persist around non-contractible loops in the network topology.

This decomposition provides a principled method for **causal ranking** of network nodes. By projecting the observed edge flow onto the gradient component, one obtains a **Hodge rank** for each node that reflects its position in the causal hierarchy. Nodes with high Hodge ranks are upstream causal drivers; nodes with low ranks are downstream effects. This approach was developed by Jiang and coauthors in the **NOCURL** algorithm for causal discovery on directed networks and has been extended by El-Yaagoubi, Chung, and Ombao in their **Causality-Based Topological Ranking (CBTR)** method for brain network analysis.

#### 4.2.2 CBTR: Integrating Causal Inference with Hodge Decomposition

The CBTR method addresses a fundamental limitation of traditional TDA in neuroscience: persistent homology relies on symmetric distance measures (cross-correlation, partial correlation, coherence) that cannot capture directional dynamics. CBTR integrates **causal inference** (specifically, Granger causality or transfer entropy) to assess effective brain connectivity with **Hodge decomposition** to rank brain regions based on their mutual influence.

The algorithm proceeds in three stages. First, a **causal inference method** (such as Granger causality or a model-based directed measure) is applied to multivariate time series data to estimate a directed edge weight matrix representing the strength of causal influence between pairs of brain regions. Second, the **Hodge decomposition** is applied to this directed network to separate the causal flow into gradient, curl, and harmonic components. Third, the **gradient component** is used to compute a **topological ranking** of brain regions, identifying the most influential regions in the causal hierarchy.

In applications to EEG data during seizures, CBTR effectively identifies brain regions showing the most significant interaction changes during ictal events. The Hodge decomposition reveals that seizure activity is associated with a breakdown of the normal gradient structure of causal flow and an increase in curl (feedback) components, suggesting a shift from hierarchical to recurrent processing patterns. These insights are not obtainable from traditional symmetric connectivity measures or from scalar summaries of causal influence.

#### 4.2.3 NOCURL and the Projection to Acyclic Graphs

The **NOCURL** algorithm addresses the problem of learning a DAG from a cyclic directed graph. Many causal discovery methods first estimate a fully connected or densely connected directed graph and then must prune it to enforce acyclicity. NOCURL uses a two-step procedure: first find an initial cyclic solution, then employ Hodge decomposition to learn an acyclic graph by projecting the cyclic graph to the gradient of a potential function. The gradient component of the edge flow corresponds to an acyclic orientation of the network, while the curl and harmonic components are discarded as cyclic artifacts.

This approach is related to the broader problem of **topological sorting** in causal discovery. In a DAG, a **topological ordering** is a linear ordering of nodes such that every edge points from an earlier to a later node in the ordering. The existence of a topological ordering is equivalent to the acyclicity of the graph. Score-based causal discovery algorithms such as **SCORE** (Rolland et al.) and its successors **DAS**, **NoGAM**, and **CAM** exploit this property by first estimating a topological ordering and then pruning the resulting fully connected DAG. Hodge decomposition provides an alternative route to topological ordering by using the gradient potential as a natural ranking function.

### 4.3 Sheaf-Theoretic and Topos-Theoretic Causal Models

Perhaps the most theoretically ambitious intersection of CI and topology arises from the application of **sheaf theory** and **topos theory** to causal inference. This line of work, primarily developed by Mahadevan and collaborators, aims to generalize Pearl's do-calculus using the machinery of higher-order category theory.

#### 4.3.1 From Graphs to Simplicial Sets: Universal Causality

In the **Universal Causality (UCLA)** framework, Mahadevan models causal interventions using **simplicial sets**, which are combinatorial objects from algebraic topology that generalize graphs to higher-dimensional relationships. A simplicial set is a contravariant functor from the category of ordinal numbers $\Delta$ to the category of sets. In this framework, 0-simplices correspond to variables, 1-simplices to causal arrows, and $n$-simplices to higher-order interactions among $n+1$ variables.

Causal interventions are modeled as **face operators** that map $n$-simplices to lower-dimensional simplices. Specifically, the face operator $d_i$ removes the $i$-th vertex from a simplex, corresponding to the marginalization or intervention on a variable. This formalism provides a hierarchical language for expressing interventions on groups of variables of arbitrary sizes, generalizing the do-operator from single-variable interventions to multi-variable, higher-order interventions.

The UCLA framework defines **causal inference as a lifting problem** in a commutative diagram whose objects are categories and whose morphisms are functors characterized as different types of fibrations. This abstract formulation captures the fundamental operation of causal inference: given partial information about a causal model (represented as a horn of a simplicial object), find a complete causal model (an extension of the horn to a full simplex) that is consistent with the observed data. This perspective unifies constraint-based causal discovery (filling inner horns through weak Kan extensions) with more general causal inference problems (filling outer horns through $\infty$-category theory).

#### 4.3.2 Topos Causal Models and the J-Do Calculus

Building on the UCLA framework, Mahadevan introduced **Topos Causal Models (TCMs)** in a NeurIPS 2025 Spotlight paper. A topos is a category that behaves like the category of sets and functions, providing a generalized universe in which to do mathematics. TCMs generalize SCMs by building on the topos theory of sheaves. The key insight is that Pearl's condition that local functions "glue together" to form a unique global function is precisely the **sheaf condition**.

In TCMs, causal interventions are modeled not as graph surgery but as **subobject classifiers** in a topos. A subobject classifier $\Omega$ is an object with a special morphism $\text{true}: 1 \to \Omega$ such that every monic arrow (subobject) corresponds uniquely to a characteristic function into $\Omega$. This provides an intuitionistic logic for causal claims, where truth is **local** rather than global. Mahadevan develops an **intuitionistic j-do calculus** ("Judo calculus") that generalizes Pearl's three rules to a more general axiomatic framework using **Lawvere-Tierney topologies** on the topos.

The central theorem establishes that **any causal functor** from a structural causal category to a semantic category (such as probability spaces) **factors uniquely through a TCM structure** defined by the Yoneda embedding. This universality result shows that TCMs are not merely a generalization of SCMs but a **canonical representation** that captures all possible causal inference structures.

#### 4.3.3 HOLOGRAPH: Sheaf-Theoretic Causal Discovery with LLMs

The **HOLOGRAPH** framework (Kim, 2025) applies sheaf theory to the practical problem of causal discovery, with a focus on integrating prior knowledge from **large language models (LLMs)**. The key insight is that local causal beliefs about subsets of variables can be formalized as **sections of a presheaf** over the power set of variables. A coherent global causal structure corresponds to the existence of a **global section** satisfying the sheaf descent conditions, while contradictions or missing information manifest as **topological obstructions** measured by **sheaf cohomology**.

HOLOGRAPH introduces several novel technical contributions. The **Algebraic Latent Projection** handles hidden confounders by projecting global causal models onto observed subsets while accounting for latent variables. **Natural gradient descent** on the belief manifold provides principled optimization with Tikhonov regularization for numerical stability. **Expected Free Energy (EFE)**-based query selection enables active learning by choosing maximally informative LLM queries that balance epistemic and instrumental value.

Perhaps the most striking finding from the HOLOGRAPH experiments is the **systematic failure of the Locality axiom**. While Identity, Transitivity, and Gluing axioms are satisfied to numerical precision ($<10^{-6}$), the Locality axiom fails with errors of $\mathcal{O}(1)$ to $\mathcal{O}(3)$ depending on graph size. The authors interpret this not as a bug but as a fundamental feature: "it reveals fundamental non-local information propagation through latent confounders, which cannot be captured by purely local restrictions." This failure suggests that the presheaf of causal models over acyclic directed mixed graphs (ADMGs) is **not a sheaf in the classical sense**, motivating future work on **non-commutative cohomology** for causal inference.

#### 4.3.4 Sheaf-Theoretic Causal Emergence

Krasnovsky (2025) combines **cellular sheaves** with **causal emergence analysis** to evaluate system resilience in distributed networks. Causal emergence, a concept introduced by Hoel and colleagues, quantifies whether macro-level dynamics (coarse-grained groupings) exhibit stronger causal efficacy than micro-level dynamics. In Krasnovsky's framework, a distributed system is modeled as a graph with attributes, and a cellular sheaf formalizes how local interactions compose into global states. Flow simulations propagate functional loads and failures, and **effective information (EI)** metrics compare the predictive power of micro-level versus macro-level descriptions.

If the macro-level EI exceeds the micro-level EI, the system exhibits **causal emergence** at that grouping, suggesting a resilient macro-scale structure. A **causal resilience index** $R_{\text{cause}} = EI_{\text{macro}} - EI_{\text{micro}}$ quantifies this emergence. The sheaf structure ensures that macro-level assignments satisfy local-to-global consistency constraints, providing a principled way to detect and validate causal emergence. Applications include microservices architectures, neural networks, and power grids.

### 4.4 Higher-Order Category Theory for Causal Inference

Closely related to the sheaf-theoretic approaches, a line of work uses **higher-order category theory** to unify causal inference with other learning paradigms and to model higher-order causal interactions that go beyond pairwise relationships.

#### 4.4.1 Simplicial Objects for Causal and Decision Models

In Mahadevan's framework for **unifying causal inference and reinforcement learning**, both structure discovery problems are formulated in terms of **simplicial objects**. A simplicial object $X_n$ ($n \geq 0$) is a contravariant functor from the category of ordinal numbers into an underlying category encoding a universal causal model or a universal decision model. The 0th order simplices are variables or states; 1-simplices are arrows encoding directional relationships; and higher-dimensional simplices encode higher-order relationships including symmetries and collective interactions.

**Causal horns** are defined as fragments of causal models that are equivalent under conditional independence: an **inner horn** $\Lambda_k^n$ is a subset of an $n$-simplex obtained by removing the interior and the face opposite the $k$-th vertex. Filling an inner horn corresponds to discovering a latent causal structure consistent with observed conditional independences. **Predictive state horns** are fragments of potential tests in predictive state representations for dynamical systems. Both types of horns are special cases of the horn-filling problem in higher-order category theory, and their solutions correspond to **Kan extensions**, **quasicategories**, and ultimately **$\infty$-categories** depending on the complexity of the structure being discovered.

#### 4.4.2 Nerves of Categories and Homotopy Colimits

The **nerve of a category** is a fully faithful functor from a category to its associated simplicial object. It provides a lossless encoding of a category as a simplicial object, in contrast to the left adjoint (the **realization** functor), which is destructive and only preserves information up to 2-simplices. Causal discovery can be posed as the problem of finding the nerve of the true causal category from observed data, which is a form of **homotopy colimit** problem.

The **homotopy layer** of the UCLA framework characterizes causal models in terms of homotopy colimits defined on the nerve of a category. This provides a way to compare causal models up to **homotopy equivalence**: two causal models are equivalent if their nerves are connected by a zigzag of weak equivalences. This notion of equivalence is coarser than graph isomorphism but finer than Markov equivalence, potentially providing new identifiability results for causal discovery.

#### 4.4.3 Causal Dynamics on Simplicial Complexes

The **Causal Dynamics of Simplicial Complexes (CDSC)** framework, introduced by Arrighi and Martiel, extends the theory of **causal graph dynamics** to discrete surfaces represented as simplicial complexes. In this model, causal evolution rules are local maps on simplicial complexes that preserve certain topological properties, including **rotation-commutation** and **bounded-star preservation**. These conditions ensure that information does not propagate too fast and that geometrical distances can be mapped into graph distances.

While CDSC is motivated by quantum gravity and fundamental physics rather than statistical applications, it provides a rigorous mathematical framework for **dynamical causal systems on topological spaces**. The decidability results for the CDSC properties suggest that certain topological constraints on causal dynamics can be algorithmically verified, which may have implications for validating causal models in applications where temporal and spatial topology are coupled.

### 4.5 Topological Ordering in Causal Discovery

A significant body of work exploits the **topological ordering** of directed acyclic graphs for scalable causal discovery. While "topological ordering" in this context refers to the graph-theoretic ordering of nodes in a DAG rather than to topological data analysis per se, the mathematical connection to order theory and the algorithmic innovations in this area are relevant to the broader TCDA agenda.

#### 4.5.1 Score-Based Topological Ordering

The **SCORE** algorithm (Rolland et al.) demonstrated that the **topological order** of a causal DAG can be recovered from the **Hessian of the data log-likelihood** (or the score function) under additive noise models. Specifically, for an ANM where each variable is a function of its parents plus independent noise, the diagonal elements of the score Hessian have minimum variance at leaf nodes. By iteratively identifying leaves and removing them from the graph, SCORE recovers a topological ordering in $\mathcal{O}(d^2)$ evaluations of the score function.

Subsequent work has dramatically improved the scalability and accuracy of this approach. **DAS** (Montagna et al.) provides a more efficient pruning step that inherits the ordering method from SCORE but achieves better scaling by using the score Jacobian to directly identify parent sets. **NoGAM** generalizes the score-matching procedure to nonlinear causal mechanisms with **arbitrary noise distributions**, removing the Gaussian noise assumption. **SSTS** (Score-Schur Topological Sort) extracts topological order directly from unconstrained generative models using the **Schur complement** of the Score-Jacobian Information Matrix, achieving scalability to graphs with up to 1000 variables.

#### 4.5.2 Information-Theoretic Topological Ordering

The **TOPIC** framework (Xu, Mameche, and Vreeken, AISTATS 2025) approaches topological ordering from an information-theoretic perspective. Inspired by Kolmogorov complexity, TOPIC proceeds in a topological order of the true graph by iteratively identifying the node for which all parents have been accounted for. An **oracle** based on compression gain determines the direction of causal edges: if adding an edge $(X, Y)$ provides greater compression than adding $(Y, X)$, then $X$ is judged to be a parent of $Y$.

TOPIC provides **full identifiability guarantees** under the assumption of algorithmic independence of conditionals and faithfulness. The framework is applicable to both i.i.d. and non-i.i.d. (multi-context) settings, making it one of the most general causal discovery methods available. On continuous, time series, and interventional data, TOPIC frequently outperforms specialized methods, demonstrating the power of information-theoretic principles for causal structure learning.

#### 4.5.3 Hybrid Top-Down Approaches

Recent work has introduced **hybrid approaches** that combine topological ordering with constraint-based pruning. The **LHTS** (Linear Hierarchical Topological Sort) and **NHTS** (Nonlinear Hierarchical Topological Sort) algorithms exploit **local causal relationships** to obtain compact hierarchical orderings that encode more causal information than linear orderings. By learning from root vertices rather than leaves, these algorithms run fewer high-dimensional regressions and use smaller conditioning sets, achieving lower sample complexity. The **ED** (Edge Discovery) algorithm nonparametrically prunes spurious edges from a discovered topological ordering, leveraging local properties to use smaller conditioning sets than traditional sparse regression techniques.

### 4.6 Mapper and Causal Feature Discovery

The final mode of intersection concerns the use of the **Mapper algorithm** for causal feature selection and subgroup discovery. While less theoretically formalized than the persistent homology and sheaf-theoretic approaches, these methods have proven valuable in applied settings.

#### 4.6.1 Mapper for Causal Feature Selection

TDA has been applied to identify **topologically important features** for causal models. The DataRefiner platform, for example, combines **gradient boosting trees** with TDA for root cause analysis in manufacturing. Mapper networks are constructed from high-dimensional process data, and key process variables are selected by analyzing the network shapes. These selected features are then used in predictive models, which achieve at least the same level of accuracy as models using all process variables, demonstrating that TDA can identify the minimal set of causally relevant features.

The approach has been successfully applied to semiconductor manufacturing processes and aircraft engine performance analysis, where datasets may involve up to 100,000 dimensions. Mapper's ability to detect subgroups of data that are selectively responsive to different process variables enables more effective process monitoring and diagnosis than traditional feature selection methods.

#### 4.6.2 Subgroup Discovery in Precision Medicine

TDA has also been applied to **subgroup discovery** in precision medicine using the Mapper algorithm. In contrast to traditional clustering techniques that group data points into disjoint clusters, Mapper represents data as a graph where nodes correspond to clusters of patients in overlapping subsets and edges represent relationships between subgroups. This graph structure can reveal **loops** (recurrent disease states), **branches** (disease progression pathways), and **voids** (absence of certain phenotypes) that are missed by standard clustering.

When applied to pathology data, Mapper offers a unique approach to subgroup discovery that emphasizes relationships and connectivity between subgroups. Integration with causal inference frameworks could enable the identification of patient subgroups that respond differently to treatments, supporting the development of personalized causal models. For example, the identification of a novel breast cancer tumor subgroup with 100% survival rate using Mapper demonstrates the potential for topology-guided causal stratification.

#### 4.6.3 Topological Hawkes Processes for Event Sequences

In the domain of **event sequence analysis**, several methods have been developed that combine topological network structures with causal point process models. The **Topological Hawkes Process (THP)** and its extensions model the generation of event sequences on networks where the topological relationships among devices influence the propagation of events. The **S2GCSL** algorithm and **CausalNET** model causal structures on event sequences with topological network information, supporting flexible event sequence modeling without the restrictive i.i.d. assumption.

These methods are particularly relevant for applications in **telecommunication network fault diagnosis**, where a single fault can trigger cascades of alarms across multiple devices within a topological network. By incorporating the network topology into the causal model, these methods achieve superior performance compared to approaches that ignore the spatial relationships among event sources.

---

## 5. Applications Across Scientific Domains

The intersection of causal inference and topological data analysis has found applications across a diverse range of scientific domains. We review the most significant applications, emphasizing how the topological perspective has enabled new insights that would be difficult to obtain with traditional methods.

### 5.1 Neuroscience and Brain Network Analysis

Neuroscience represents one of the richest application domains for TCDA. Brain networks, whether structural (from diffusion MRI), functional (from resting-state fMRI or EEG), or effective (from Granger causality or transfer entropy), are inherently complex, high-dimensional, and structured. Traditional analyses often reduce these networks to scalar summaries or pairwise connectivity matrices, discarding the rich topological and causal structure.

The **CBTR** method has demonstrated that integrating causal inference with Hodge decomposition provides novel insights into the **hierarchical organization of brain networks** during seizures. The Hodge decomposition of dynamic brain networks reveals distinct temporal patterns across gradient, curl, and harmonic components, with gradient and harmonic flows exhibiting substantial fluctuations in a compensatory manner. During seizures, the normal gradient structure of causal flow breaks down and curl (feedback) components increase, suggesting a shift from hierarchical to recurrent processing.

**Persistent homology** has been applied to characterize altered topological structures in the brain white matter of maltreated children. By comparing persistence diagrams between maltreated and typically developing children using the **Wasserstein distance**, researchers found that maltreatment increases homogeneity in white matter structures, reflected in systematic shifts in the topological profile. These effects are not detectable with standard volumetric or connectivity measures, demonstrating the unique sensitivity of topological methods.

**Higher-order effective connectivity** frameworks extend information-theoretic causal inference to capture **synergistic interactions beyond pairwise** methods. Standard measures such as transfer entropy do not distinguish between additive and truly synergistic causal structures. Refined approaches based on **partial information decomposition** capture hyperedges in causal graphs, assigning causal status to sets of variables only when their joint contribution is irreducible. This is illustrated on biophysically realistic neuronal models, including dendritic XOR computations, demonstrating **exclusive joint causality** not detectable by pairwise methods.

### 5.2 Genomics and Gene Regulatory Networks

Gene regulatory networks (GRNs) are fundamental objects of study in systems biology, representing the regulatory interactions among genes, transcription factors, and other molecular entities. Traditional GRN inference methods produce pairwise interaction networks, but biological regulation often involves **higher-order interactions** among multiple regulators.

The **CausalGRN** framework uses **topology-driven analysis** to identify significant driver genes in regulatory networks. By analyzing the topological structure of inferred GRNs, CausalGRN identifies hub nodes with disproportionate influence on network topology, such as FOXA1 and NEUROD1 in prostate cancer regulatory networks. These topological drivers often correspond to master transcriptional regulators that would not be identified by standard degree-based or expression-based rankings.

**Single-cell topological data analysis** has emerged as a powerful framework for exploring complex biological data. Methods such as **scGeom** and **Gene2role** apply TDA concepts to reveal structural characteristics of gene regulatory network modules reconstructed from single-cell omics data. The integration of TDA with machine learning, probabilistic modeling, and causal inference promises to deepen its utility by embedding topological summaries into predictive frameworks, facilitating the construction of biologically grounded models that are both data-driven and theoretically robust.

### 5.3 Precision Medicine and Healthcare

In precision medicine, the goal is to tailor treatments to individual patients based on their unique characteristics. Causal inference provides the methodological foundation for estimating heterogeneous treatment effects, while TDA offers tools for characterizing the complex patient phenotypes that drive heterogeneity.

**Subgroup discovery** using Mapper has been applied to identify patient subgroups with distinct disease trajectories or treatment responses. Unlike traditional clustering, which partitions patients into disjoint groups, Mapper produces a graph structure that reveals continuous transitions between subgroups, alternative progression pathways, and gaps in the phenotype space. When combined with causal effect estimation within each subgroup, this approach enables **topology-guided precision medicine** that respects the continuous and multifaceted nature of patient heterogeneity.

The **meta-learning for personalized causal graphs** framework addresses the challenge of learning personalized causal models with limited samples per patient. By employing a meta-learning framework that shares knowledge across a collection of correlated causal structure learning tasks, the method enables accurate personalized causal graph learning. The combination of shared and individual topology aids in the construction of personalized causal graphs, demonstrating that topological structure can be transferred across related causal learning problems.

### 5.4 Financial Systems and Crisis Detection

Financial markets are complex systems characterized by nonlinear dynamics, regime shifts, and contagion effects. The **Topological Machine Learning for Financial Crisis Detection** framework integrates TDA with a strictly causal detection pipeline to identify **early warning signals (EWS)** of financial crises. The methodology introduces **L1- and L2-norm indicators of persistence landscapes** as informative features and demonstrates their predictive power across several major crises using multiple ML classifiers.

The framework was empirically validated across multiple historical financial crises, including the 2008 global financial crisis and the 2020 COVID-19 crash, using daily stock index data. Results demonstrate that **topological indicators significantly improve predictive performance** compared to baseline models, offering a promising and interpretable tool for early crisis detection. The causal detection pipeline ensures that identified topological signals are not merely predictive but reflect genuine causal pathways through which systemic risk propagates.

### 5.5 Manufacturing and Industrial Systems

In manufacturing, root cause analysis requires identifying the causal factors behind process variations, defects, or equipment failures. The **DataRefiner** platform applies TDA to high-dimensional manufacturing data for causal feature selection and root cause analysis. By constructing Mapper networks from process data and selecting features that impact system outcomes through network shape analysis, the platform achieves prediction accuracy comparable to using all process variables while dramatically reducing model complexity.

Applications include **chemical process yield prediction** and **semiconductor wafer fault detection**, where the number of process parameters can reach into the hundreds of thousands. The topological approach enables the identification of **hidden causal structures** that are difficult to detect using conventional methods, particularly when relationships are nonlinear and involve higher-order interactions among process variables.

---

## 6. Open Problems and Research Gaps

Despite significant recent advances, the intersection of causal inference and topological data analysis remains in its early stages. We identify the most pressing open problems and research gaps that must be addressed for TCDA to mature as a distinct methodological discipline.

### 6.1 Theoretical Foundations and Identifiability

**Non-commutativity of persistent homology with mixtures.** A fundamental theoretical challenge arises from the fact that persistent homology does not commute with mixtures over covariates. As Saki and Faghihi demonstrate, a marginal persistence-diagram effect is not identified from conditional topological ignorability alone. This means that **marginal topological causal effects** cannot in general be identified from observational data, even under strong ignorability assumptions. Current frameworks address this by focusing on **conditional topological effects**, but the relationship between marginal and conditional topological effects, and the conditions under which marginal effects are identifiable, remain poorly understood.

**Topological identifiability conditions.** Classical causal inference relies on identifiability conditions such as faithfulness, causal sufficiency, and the Markov condition. The analogous conditions for topological causal models have not been fully developed. What does **topological faithfulness** mean? Under what conditions is the **topological causal structure** (rather than just the scalar causal effects) identifiable from data? These questions require new mathematical frameworks that combine causal identifiability theory with the stability theory of persistent homology.

**Consistency of topological causal discovery.** While consistency results exist for many causal discovery algorithms in the classical setting, analogous results for topology-aware causal discovery are largely absent. Under what conditions do topological causal discovery methods converge to the true causal structure as sample size increases? What are the **rates of convergence** for persistence diagram-based causal estimands?

### 6.2 Computational Challenges

**Scalability of persistent homology for causal inference.** Computing persistent homology for large samples of complex outcomes remains computationally expensive. While recent algorithms such as Ripser have dramatically improved the efficiency of persistence computation, the need to compute persistence diagrams for many conditional distributions (one for each covariate stratum) in causal effect estimation creates a multiplicative computational burden. **Approximation algorithms**, **sketching techniques**, and **distributed computation** strategies are needed to make topological causal inference practical for large-scale applications.

**Sheaf cohomology computation.** The sheaf-theoretic frameworks described above are theoretically elegant but computationally demanding. Computing sheaf cohomology for realistic causal models involves solving large systems of linear equations over cellular sheaves on high-dimensional simplicial complexes. Developing **efficient algorithms** for sheaf cohomology computation, possibly leveraging the special structure of causal sheaves, is essential for practical applications.

**Parameter selection in TDA for causal inference.** Topological data analysis involves multiple analyst degrees of freedom, including the choice of filtration, scale parameters, and topological summaries. In the causal inference context, these choices can affect both the **validity** and **efficiency** of causal estimates. Developing **data-driven methods** for parameter selection that preserve the causal interpretation of topological estimands is an important open problem.

### 6.3 Methodological Gaps

**Time-varying treatments and dynamic regimes.** Most existing topological causal inference methods are designed for static, point-treatment settings. Extensions to **time-varying treatments**, **dynamic treatment regimes**, and **sequential decision making** are largely unexplored. In these settings, the topological structure of outcomes may evolve over time, requiring methods for **persistent homology of time series** and **dynamic persistence diagrams**.

**Network interference and spillover effects.** In social, biological, and technological networks, the treatment of one unit can affect the outcomes of other units through **interference** or **spillover effects**. Topological methods are naturally suited to characterizing network structure, but the integration of interference models with topological causal inference remains undeveloped. How should persistence diagrams be defined for outcomes on networks with interference? How can Hodge decomposition be used to separate direct treatment effects from spillover effects?

**Continuous treatments and dose-response.** The extension of topological causal inference to **continuous treatments** presents both theoretical and practical challenges. For scalar outcomes, dose-response curves can be estimated using nonparametric regression or marginal structural models. For topological outcomes, the dose-response relationship is a function from the treatment space to the space of persistence diagrams, requiring new estimation and inference methods.

**Higher-order interactions and synergistic effects.** Biological and social systems often exhibit **higher-order interactions** that cannot be decomposed into pairwise effects. While partial information decomposition and related frameworks can quantify synergy and redundancy in information-theoretic terms, the integration of these measures with topological causal models remains incomplete. How can **simplicial complexes** be used to represent higher-order causal interactions? What are the appropriate topological summaries for quantifying synergistic causal effects?

### 6.4 Interpretability and Communication

**Communicating topological causal findings.** One of the strengths of classical causal inference is the interpretability of its estimands: the ATE represents the average difference in outcomes if everyone were treated versus if no one were treated. Topological causal effects, by contrast, are functions on abstract spaces (persistence diagrams, silhouette functions) that may be difficult for applied researchers to interpret. Developing **intuitive interpretations** and **visualization tools** for topological causal effects is essential for practical adoption.

**Causal attribution of topological features.** When a topological causal effect is detected, it is natural to ask which specific topological features (which loops, which connected components, which voids) are responsible for the effect. **Attribution methods** that map topological causal effects back to specific features of the data, analogous to feature importance in machine learning, would greatly enhance the practical utility of topological causal inference.

### 6.5 Integration with Machine Learning

**Deep learning with topological causal constraints.** While topological layers have been developed for neural networks (e.g., PersLay, PLLay), these layers are primarily used for predictive tasks. Integrating topological constraints into **causal machine learning** models, such as causal representation learning algorithms or generative models for counterfactuals, remains largely unexplored. Can persistent homology be used as a regularizer to enforce causal structure in deep learning models?

**Causal discovery with topological priors.** The sheaf-theoretic frameworks demonstrate that topological structure can serve as a **prior** for causal discovery. Developing practical algorithms that incorporate topological priors into causal discovery methods, possibly using **variational inference** or **expectation propagation**, could improve both the accuracy and efficiency of structure learning.

---

## 7. A Research Agenda for Topological Causal Data Analysis

Drawing on the literature review and open problem analysis above, we propose a research agenda for establishing **Topological Causal Data Analysis (TCDA)** as a distinct methodological discipline. This agenda is organized around five core pillars: theoretical foundations, computational infrastructure, methodological innovation, domain applications, and community building.

### 7.1 Theoretical Foundations

The development of TCDA requires a rigorous theoretical foundation that integrates the identifiability theory of causal inference with the stability theory of topological data analysis. Priority research directions include:

**Formalizing topological identifiability.** Develop necessary and sufficient conditions for the identification of topological causal effects from observational and experimental data. This includes defining **topological analogues** of classical identifiability concepts (faithfulness, causal sufficiency, the back-door criterion) and characterizing the **observational equivalence** of topological causal models.

**Stability of causal inference under topological perturbations.** Extend the stability theorems of persistent homology to the causal inference setting. Specifically, characterize how **perturbations to the data-generating process** (e.g., misspecification of the outcome model, measurement error) propagate through the topological causal inference pipeline to affect the estimated causal effects.

**Asymptotic theory for topological causal estimators.** Develop central limit theorems, convergence rates, and minimax lower bounds for topological causal effect estimators. This includes characterizing the **semiparametric efficiency bound** for topological causal effects and developing estimators that achieve this bound.

### 7.2 Computational Infrastructure

The practical adoption of TCDA depends on the availability of efficient, reliable, and user-friendly software. Priority directions include:

**Scalable algorithms for conditional persistent homology.** Develop algorithms that can efficiently compute persistence diagrams for a large number of conditional distributions, leveraging **approximation**, **sketching**, and **parallel computation**. Target applications include datasets with hundreds of thousands of samples and complex outcome spaces.

**Open-source software packages.** Create integrated open-source software packages that implement the full TCDA pipeline, from data preprocessing through topological causal effect estimation to visualization and interpretation. These packages should be designed for interoperability with existing causal inference software (e.g., `DoWhy`, `EconML`, `CausalML`) and TDA software (e.g., `GUDHI`, `Ripser`, `scikit-tda`).

**Benchmark datasets and evaluation protocols.** Develop benchmark datasets with known topological causal structure for evaluating and comparing TCDA methods. These benchmarks should span multiple application domains and should include both synthetic data with ground-truth topological effects and real-world data with validated causal findings.

### 7.3 Methodological Innovation

The field of TCDA is ripe for methodological innovation at the intersection of topology and causality. Priority directions include:

**Topological mediation analysis.** Develop methods for decomposing topological causal effects into **direct** and **indirect** (mediated) components. This requires defining topological analogues of the natural direct effect and natural indirect effect, and developing estimation strategies that respect the nonlinearity of persistent homology.

**Topology-aware causal discovery.** Integrate topological information into causal discovery algorithms. For example, persistent homology could be used to identify **higher-order causal interactions** that are missed by pairwise methods, or Mapper could be used to identify **causal subgroups** that are then used to constrain the search space of causal discovery algorithms.

**Dynamic topological causal models.** Extend TCDA to **temporal settings** where both the causal structure and the topological structure of outcomes evolve over time. This includes developing methods for **persistent homology of time series**, **dynamic persistence diagrams**, and **online topological causal inference**.

### 7.4 Domain-Specific Development

While TCDA is a general methodology, its development will be driven by applications in specific scientific domains. Priority directions include:

**Neuroscience.** Develop TCDA methods tailored to **neuroimaging data**, including fMRI, EEG, and diffusion MRI. Specific challenges include the high dimensionality of neuroimaging data, the temporal dynamics of brain activity, and the need to integrate structural, functional, and effective connectivity measures.

**Genomics and systems biology.** Apply TCDA to **gene regulatory network inference**, **single-cell analysis**, and **protein structure prediction**. Specific challenges include the noise and sparsity of genomic data, the need to model higher-order regulatory interactions, and the integration of multiple data modalities (transcriptomics, proteomics, epigenomics).

**Climate and environmental science.** Apply TCDA to **climate teleconnection networks**, **ecosystem dynamics**, and **environmental health**. Specific challenges include the spatial and temporal autocorrelation of environmental data, the need to model feedback loops and tipping points, and the integration of physical process models with data-driven topological methods.

### 7.5 Community Building and Education

The maturation of TCDA as a discipline requires the cultivation of a diverse community of researchers, practitioners, and educators. Priority directions include:

**Interdisciplinary training programs.** Develop graduate curricula and summer schools that provide rigorous training in both causal inference and topological data analysis. These programs should emphasize the **integration** of the two fields rather than treating them as separate subjects.

**Collaborative research networks.** Establish research networks that bring together statisticians, computer scientists, mathematicians, and domain scientists to work on TCDA problems. These networks should include both theoretical and applied researchers, and should prioritize the inclusion of early-career researchers and researchers from underrepresented groups.

**Open science practices.** Promote open science practices in TCDA research, including the publication of open-source software, the sharing of benchmark datasets, and the preregistration of studies. These practices will accelerate the development and validation of TCDA methods and will ensure that the benefits of TCDA are widely accessible.

---

## 8. Conclusion

This review has documented the emergence of a new methodological discipline at the intersection of causal inference and topological data analysis. We have identified six primary modes of intersection: persistent homology for causal effect estimation, Hodge decomposition for causal ranking, sheaf-theoretic causal models, higher-order category theory for causal inference, topological ordering in causal discovery, and Mapper for causal feature discovery. We have cataloged applications across neuroscience, genomics, precision medicine, finance, and manufacturing, and we have identified critical open problems including the non-commutativity of persistent homology with covariate mixtures, computational scalability, and the need for topological identifiability conditions.

The convergence of these two fields is not merely a technical development but a reconceptualization of what causal inference can be. Traditional causal inference treats outcomes as points in a Euclidean space and asks how interventions shift the expected location of these points. Topological causal data analysis treats outcomes as shapes and asks how interventions alter their geometry, connectivity, and topology. This shift in perspective opens new avenues for scientific discovery, enabling researchers to detect and quantify causal effects that are invisible to traditional methods.

The establishment of Topological Causal Data Analysis as a distinct discipline will require sustained investment in theoretical foundations, computational infrastructure, methodological innovation, domain applications, and community building. We believe that this investment is warranted by the scientific potential of the field and by the growing recognition that many of the most important causal questions in modern science concern not just the magnitude of effects but their structure.

---

## 9. References

1. Kim, K. & Lee, H. (2025). Topological Causal Effects. *Proceedings of the International Conference on Learning Representations (ICLR)*. https://arxiv.org/abs/2603.02289

2. Saki, A. & Faghihi, U. (2026). Beyond Means: Topological Causal Effects under Persistent-Homology Ignorability. *arXiv preprint*. https://arxiv.org/abs/2603.14169

3. El-Yaagoubi, A.B., Chung, M.K. & Ombao, H. (2024). Topological Analysis of Seizure-Induced Changes in Brain Hierarchy Through Effective Connectivity. *arXiv preprint*. https://arxiv.org/abs/2407.13514

4. Mahadevan, S. (2025). Universal Causal Inference in a Topos of Sheaves. *Advances in Neural Information Processing Systems (NeurIPS)* 38.

5. Kim, H. (2025). HOLOGRAPH: Active Causal Discovery via Sheaf-Theoretic Alignment of Large Language Model Priors. *arXiv preprint*. https://arxiv.org/abs/2512.24478

6. Krasnovsky, A.A. (2025). Sheaf-Theoretic Causal Emergence Analysis. *arXiv preprint*. https://arxiv.org/abs/2503.14104

7. Mahadevan, S. (2022). Unifying Causal Inference and Reinforcement Learning using Higher-Order Category Theory. *arXiv preprint*.

8. Mahadevan, S. (2023). Universal Causality: A Layered Architecture. *Entropy*.

9. Xu, S., Mameche, S. & Vreeken, J. (2025). Information-Theoretic Causal Discovery in Topological Order. *Proceedings of AISTATS* 258:2008-2016.

10. Rolland, P., et al. (2022). Score Matching Enables Causal Discovery of Nonlinear Additive Noise Models. *International Conference on Machine Learning (ICML)*.

11. Montagna, D., et al. (2023). Scalable Causal Discovery with Score Matching. *Proceedings of UAI*.

12. Wu, R. & Xie, H. (2026). Optimization-Free Topological Sort for Causal Discovery via the Schur Complement of Score Jacobians. *arXiv preprint*. https://arxiv.org/abs/2604.25295

13. Jiang, Y., et al. NOCURL: Hodge Decomposition for Non-convex Optimization and Cycle Detection in Causal Discovery. *Journal of Machine Learning Research*.

14. Bailey, M.M. (2026). Topology as a Language for Emergent Organization in Complex Systems: Multiscale Structure, Higher-Order Interactions, and Early Warning Signals. *arXiv preprint*. https://arxiv.org/abs/2603.25760

15. Pearl, J. (2009). *Causality: Models, Reasoning, and Inference* (2nd ed.). Cambridge University Press.

16. Imbens, G.W. & Rubin, D.B. (2015). *Causal Inference in Statistics, Social, and Biomedical Sciences*. Cambridge University Press.

17. Chazal, F. & Michel, B. (2021). An Introduction to Topological Data Analysis: Fundamental and Practical Aspects for Data Scientists. *Foundations and Trends in Machine Learning*.

18. Carlsson, G. (2009). Topology and Data. *Bulletin of the American Mathematical Society* 46(2):255-308.

19. Ghrist, R. (2014). *Elementary Applied Topology*. CreateSpace Independent Publishing Platform.

20. Hoel, E.P., Albantakis, L. & Tononi, G. (2013). Quantifying Causal Emergence Shows that Macro Can Beat Micro. *Proceedings of the National Academy of Sciences* 110(49):19790-19795.

---

**Acknowledgments.** This review was prepared to support the development of a novel research domain called Topological Causal Data Analysis (TCDA). The authors thank the broader causal inference and topological data analysis communities for their pioneering work at this intersection.
