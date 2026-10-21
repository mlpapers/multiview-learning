# Multi-view learning

## Overview

- **[A Survey on Multi-view Learning](https://arxiv.org/abs/1304.5634)** (Xu et al., 2013, preprint). Organizes learning from multiple descriptions of the same objects into co-training, multiple kernel learning, and shared subspaces; distinguishes agreement from complementary information.

## Co-training and label acquisition

- **[Co-training](https://www.cs.cmu.edu/~avrim/Papers/cotrain.pdf)** (Blum & Mitchell, 1998). Classifiers trained on separate views exchange confident labels for unlabeled examples. The original guarantee assumes each view is sufficient and the views are conditionally independent given the label.
- **[Analyzing Co-training](https://doi.org/10.1145/354756.354805)** (Nigam & Ghani, 2000). Examines how view independence and feature splits affect co-training; introduces co-EM, which exchanges probabilistic labels between views rather than committing to selected hard labels.
- **[Co-regularized Least Squares](https://doi.org/10.1145/1143844.1143862)** (Brefeld et al., 2006). Couples view-specific regressors through an agreement penalty on unlabeled examples. A semiparametric approximation reduces the cost of using a large unlabeled set.
- **[Active Learning with Multiple Views](https://arxiv.org/abs/1110.1073)** (Muslea et al., JAIR 2006; arXiv 2011). Co-Testing requests labels for examples on which view-specific classifiers disagree, combining multiple views with active label acquisition.

## Shared representations

### Correlation-based projections

- **[CCA](https://doi.org/10.1093/biomet/28.3-4.321)** (Hotelling, 1936). Finds linear projections of two paired variable sets with maximal correlation. [scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.cross_decomposition.CCA.html) provides fitting and transforms for new samples.
- **[Generalized CCA](https://doi.org/10.1093/biomet/58.3.433)** (Kettenring, 1971). Compares five extensions of canonical analysis to three or more variable sets, including summed-correlation and maximum-variance objectives; these criteria need not yield the same solution.
- **[Kernel CCA: Convergence Analysis](https://link.springer.com/article/10.1007/s10994-008-5085-3)** (Hardoon & Shawe-Taylor, 2009). Analyzes generalization and regularization for correlation maximization in kernel feature spaces, allowing nonlinear relationships between paired views.
- **[Deep CCA](https://proceedings.mlr.press/v28/andrew13.html)** (Andrew et al., 2013). Learns a nonlinear encoder for each of two views by maximizing correlation between their outputs. Paired training observations define the cross-view correspondence.
- **[Deep CCA Autoencoders](https://proceedings.mlr.press/v37/wangb15.html)** (Wang et al., 2015). Combines cross-view correlation with reconstruction of each input view; compares correlation-based, reconstruction-based, and hybrid objectives for representations used downstream.
- **[Deep Generalized CCA](https://aclanthology.org/W19-4301/)** (Benton et al., 2017 preprint; 2019 workshop). Extends nonlinear correlation-based representation learning beyond two views through view-specific networks and a shared latent representation.
- **[Multi-view nonlinear ICA](https://proceedings.mlr.press/v115/gresele20a.html)** — 2019/2020. Gresele et al. identify independent latent sources from sufficiently different noisy nonlinear views under their corruption assumptions. Multiple views supply identifying information; maximizing correlation alone is a different objective.

### Shared and view-specific factors

- **[MOFA](https://www.embopress.org/doi/full/10.15252/msb.20178124)** (Argelaguet et al., 2018). Bayesian factor analysis separates variation shared across omics assays from variation specific to individual assays; supports incomplete measurements on overlapping samples.
- **[MOFA+](https://link.springer.com/article/10.1186/s13059-020-02015-1)** (Argelaguet et al., 2020). Extends MOFA to multiple sample groups and modalities with flexible sparsity and scalable variational inference, including applications to single-cell data.

## Supervised projections and metrics

- **[Multi-view Fisher Discriminant Analysis](https://link.springer.com/chapter/10.1007/978-3-642-15880-3_27)** (Diethe et al., 2010). Extends kernel Fisher discrimination to aligned views, with sparse and private-direction variants for supervised classification.
- **[Generalized Multiview Analysis](https://users.umiacs.umd.edu/~hal3/docs/daume12gma.pdf)** (Sharma et al., 2012). Learns a discriminative latent space for heterogeneous views using class labels; supports cross-view classification and retrieval with linear and kernel formulations.
- **[Multiview Metric Learning](https://vipl.ict.ac.cn/publications/earlier/jour/202212/P020221231570717241981.pdf)** (Zhai et al., 2012). Combines cross-view correspondence with within-view local smoothness; learns mappings into a shared space for previously unseen samples.

## Multiple kernel learning

- **[Multiple Kernel Learning Algorithms](https://jmlr.org/papers/v12/gonen11a.html)** (Gönen & Alpaydın, 2011). Surveys kernel combination rules and learning objectives. Kernels can encode distinct views, feature subsets, or similarity functions over the same observations.
- **[MARK](https://doi.org/10.1145/775047.775051)** (Bennett et al., 2002). Builds heterogeneous kernel models through boosting and kernel column generation, selecting basis functions from multiple kernels during learning.
- **[SimpleMKL](https://jmlr.org/papers/v9/rakotomamonjy08a.html)** (Rakotomamonjy et al., 2008). Learns a sparse convex combination of kernels jointly with an SVM, alternating classifier optimization and updates of kernel weights.

## Graph fusion and clustering

- **[Co-regularized Spectral Clustering](https://proceedings.neurips.cc/paper/2011/hash/31839b036f63806cba3f47b93af8ccb5-Abstract.html)** (Kumar et al., 2011). Couples spectral embeddings of view-specific similarity graphs through agreement penalties, rather than concatenating raw features.
- **[Multi-view Clustering via Joint NMF](https://www.microsoft.com/en-us/research/wp-content/uploads/2013/05/sdm13multiview.pdf)** (Liu et al., 2013). Factorizes nonnegative views while encouraging their cluster representations toward a common consensus; retains a separate basis for each view.
- **[Similarity Network Fusion](https://www.nature.com/articles/nmeth.2810)** (Wang et al., 2014). Constructs a sample-similarity network for each data type and iteratively fuses the networks. Views share sample identities, while their feature sets can differ.

## Missing views

- **[Partial Multi-View Clustering](https://ojs.aaai.org/index.php/AAAI/article/view/8973)** (Li et al., 2014). Learns a common subspace from two partially overlapping views, using paired examples to connect them; neither view must contain every example.
- **[Multimodal VAE](https://arxiv.org/abs/1802.05335)** (Wu & Goodman, 2018). Uses a product-of-experts inference network and subsampled training to infer shared latent variables from different subsets of modalities; models joint generation and missing-modality inference.
- **[COMPLETER](https://openaccess.thecvf.com/content/CVPR2021/html/Lin_COMPLETER_Incomplete_Multi-View_Clustering_via_Contrastive_Prediction_CVPR_2021_paper.html)** (Lin et al., 2021). Combines contrastive agreement with dual prediction between latent views, recovering missing representations for incomplete multi-view clustering.
- **[Mixture-of-experts multimodal VAEs](https://arxiv.org/abs/1911.03393)** — 2019. Uses a mixture-of-experts variational posterior for multimodal generative learning, aiming to separate shared and modality-specific factors and support joint and cross-modal generation.

## Cross-modal alignment and fusion

- **[Contrastive Multiview Coding](https://arxiv.org/abs/1906.05849)** (Tian et al., 2019 preprint; ECCV 2020). Contrasts matching views of a scene against mismatched observations, learning representations of shared information across multiple sensory channels.
- **[CLIP](https://proceedings.mlr.press/v139/radford21a.html)** (Radford et al., 2021). Trains image and text encoders to identify matching pairs within a batch. Their shared space supports text–image retrieval and classification using text descriptions of classes.
- **[ImageBind](https://openaccess.thecvf.com/content/CVPR2023/html/Girdhar_ImageBind_One_Embedding_Space_To_Bind_Them_All_CVPR_2023_paper.html)** (Girdhar et al., 2023). Connects six modalities through image-paired training data; alignment does not require training pairs for every pair of modalities.
- **[Multimodal Transformer](https://aclanthology.org/P19-1656/)** (Tsai et al., 2019). Uses directional cross-modal attention to fuse language, audio, and visual sequences without explicit time-step alignment. Modalities still describe the same example.
- **[Tensor Fusion Network](https://arxiv.org/abs/1707.07250)** — 2017. Forms an outer-product tensor from augmented language, visual and acoustic embeddings, explicitly representing unimodal, pairwise and three-way interactions.
- **[Gated Multimodal Units](https://arxiv.org/abs/1702.01992)** — 2017. Learns multiplicative gates that control each modality's contribution to a fused representation; demonstrated with text and images for movie-genre prediction.

## View selection and evaluation

- **[InfoMin](https://arxiv.org/abs/2005.10243)** (Tian et al., 2020). Studies contrastive view selection: reduce shared information while retaining information needed for the downstream task. Removing task-relevant content violates this principle.
- **[Gradient-Blending](https://openaccess.thecvf.com/content_CVPR_2020/html/Wang_What_Makes_Training_Multi-Modal_Classification_Networks_Hard_CVPR_2020_paper.html)** (Wang et al., 2020). Finds that joint models can underperform individual modalities on video benchmarks; weights training losses using estimates of overfitting and generalization across modalities.
- **[MultiBench](https://arxiv.org/abs/2107.07502)** (Liang et al., 2021). Benchmarks multimodal prediction across domains, measuring task performance, training/inference cost, and robustness to noisy or missing modalities.
- **Recommended comparisons.** Test the best individual view, feature concatenation, and prediction fusion alongside the proposed method. Report each view's contribution and performance under missing or corrupted inputs. [MultiBench](https://arxiv.org/abs/2107.07502).
- **Recommended protocol.** Split by object or subject while keeping its views together. Record views available during training and deployment; evaluate held-out correlation and downstream utility separately. [DCCA evaluation](https://proceedings.mlr.press/v37/wangb15.html), [CCA-Zoo](https://jameschapman19.github.io/cca_zoo/).

## Software

- **[mvlearn](https://github.com/mvlearn/mvlearn)** — Python implementations for multi-view decomposition, clustering, and semi-supervised learning with a scikit-learn-style API. [Paper](https://arxiv.org/abs/2005.11890) (Perry et al., 2020 preprint; JMLR 2021).
- **[CCA-Zoo](https://github.com/jameschapman19/cca_zoo)** — Linear, regularized, kernel, deep, and probabilistic CCA implementations. Separate multi-view model-selection utilities preserve sample correspondence. [Documentation](https://jameschapman19.github.io/cca_zoo/).
- **[MKLpy](https://mklpy.readthedocs.io/en/latest/)** — Python kernel construction, normalization, combination, and evaluation; includes EasyMKL and GRAM. Check the implementation status of individual algorithms in its documentation.
- **[MOFA2 / mofapy2](https://biofam.github.io/MOFA2/)** — R and Python tools for multi-omics factor analysis on the same or overlapping sample sets, including multi-group models and analysis of learned factors.
- **[MultiBench code](https://github.com/human-ai-lab/multibench)** — Data loaders, fusion methods, training routines, and evaluation tools for multimodal prediction benchmarks.
- **[multiview](https://github.com/mariceli3/multiview)** — Python multi-view MDS, t-SNE, and spectral clustering. Distinct from mvlearn. [Package](https://pypi.org/project/multiview/).
- **[Multiview-FDA](https://github.com/tdiethe/Multiview-FDA)** — MATLAB routines for multi-view Fisher discrimination, citing Diethe et al.'s 2010 work on nonlinear discriminants from multiple data views.

## Related topics

- [Feature Extraction](https://mlpapers.org/feature-extraction/) — Feature maps, pretrained encoders, and dimensionality reduction.
- [Ensemble Learning](https://mlpapers.org/ensemble-learning/) — Combining predictors, including those trained on the same feature set.
- [Missing Data](https://mlpapers.org/missing-data/) — Missingness assumptions, imputation, and incomplete-data evaluation.
