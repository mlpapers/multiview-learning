# Multi-View Learning

## Overview

- **A Survey on Multi-view Learning** - Organizes learning from multiple descriptions of the same objects into co-training, multiple kernel learning, and shared subspaces; distinguishes agreement from complementary information. [Xu et al. 2013](<https://arxiv.org/abs/1304.5634> "A Survey on Multi-view Learning; arXiv").

## Co-training and label acquisition

- **Co-training** - Classifiers trained on separate views exchange confident labels for unlabeled examples. The original guarantee assumes each view is sufficient and the views are conditionally independent given the label. [Blum and Mitchell 1998](<https://www.cs.cmu.edu/~avrim/Papers/cotrain.pdf> "Combining labeled and unlabeled data with co-training; COLT").
    - **Analyzing Co-training** - Examines how view independence and feature splits affect co-training; introduces co-EM, which exchanges probabilistic labels between views rather than committing to selected hard labels. [Nigam and Ghani 2000](<https://doi.org/10.1145/354756.354805> "Analyzing the effectiveness and applicability of co-training; CIKM").
- **Co-regularized Least Squares** - Couples view-specific regressors through an agreement penalty on unlabeled examples. A semiparametric approximation reduces the cost of using a large unlabeled set. [Brefeld et al. 2006](<https://doi.org/10.1145/1143844.1143862> "Efficient co-regularised least squares regression; ICML").
- **Active Learning with Multiple Views** - Co-Testing requests labels for examples on which view-specific classifiers disagree, combining multiple views with active label acquisition. [Muslea et al. 2006](<https://arxiv.org/abs/1110.1073> "Active Learning with Multiple Views; JAIR").

## Shared representations

### Correlation-based projections

- **CCA** - Finds linear projections of two paired variable sets with maximal correlation. scikit-learn provides fitting and transforms for new samples. [Hotelling 1936](<https://doi.org/10.1093/biomet/28.3-4.321> "Relations Between Two Sets of Variates; Biometrika"); [docs](<https://scikit-learn.org/stable/modules/generated/sklearn.cross_decomposition.CCA.html>).
- **Generalized CCA** - Compares five extensions of canonical analysis to three or more variable sets, including summed-correlation and maximum-variance objectives; these criteria need not yield the same solution. [Kettenring 1971](<https://doi.org/10.1093/biomet/58.3.433> "Canonical analysis of several sets of variables; Biometrika").
- **Kernel CCA: Convergence Analysis** - Analyzes generalization and regularization for correlation maximization in kernel feature spaces, allowing nonlinear relationships between paired views. [Hardoon and Shawe-Taylor 2008](<https://link.springer.com/article/10.1007/s10994-008-5085-3> "Convergence analysis of kernel Canonical Correlation Analysis: theory and practice; Mach. Learn.").
- **Deep CCA** - Learns a nonlinear encoder for each of two views by maximizing correlation between their outputs. Paired training observations define the cross-view correspondence. [Andrew et al. 2013](<https://proceedings.mlr.press/v28/andrew13.html> "Deep Canonical Correlation Analysis; ICML").
    - **Deep CCA Autoencoders** - Combines cross-view correlation with reconstruction of each input view; compares correlation-based, reconstruction-based, and hybrid objectives for representations used downstream. [Wang et al. 2015](<https://proceedings.mlr.press/v37/wangb15.html> "On Deep Multi-View Representation Learning; ICML").
    - **Deep Generalized CCA** - Extends nonlinear correlation-based representation learning beyond two views through view-specific networks and a shared latent representation. [Benton et al. 2019](<https://aclanthology.org/W19-4301/> "Deep Generalized Canonical Correlation Analysis; RepL4NLP").
- **Multi-view nonlinear ICA** - Gresele et al. identify independent latent sources from sufficiently different noisy nonlinear views under their corruption assumptions. Multiple views supply identifying information; maximizing correlation alone is a different objective. [Gresele et al. 2020](<https://proceedings.mlr.press/v115/gresele20a.html> "The Incomplete Rosetta Stone problem: Identifiability results for Multi-view Nonlinear ICA; UAI").
- **Unpaired CCA** - Fits linear CCA projections after a QAP-based proxy pairing. Correlation-recovery theory assumes the true pairing maximizes correlation and a singular-value majorization condition; the practical matching solver is approximate. [Ben-Ari et al. 2026](<https://arxiv.org/abs/2610.09530v1> "Unpaired Canonical Correlation Analysis; NeurIPS").

### Shared and view-specific factors

- **MOFA** - Bayesian factor analysis separates variation shared across omics assays from variation specific to individual assays; supports incomplete measurements on overlapping samples. [Argelaguet et al. 2018](<https://www.embopress.org/doi/full/10.15252/msb.20178124> "Multi‐Omics Factor Analysis—a framework for unsupervised integration of multi‐omics data sets; Mol Syst Biol").
    - **MOFA+** - Extends MOFA to multiple sample groups and modalities with flexible sparsity and scalable variational inference, including applications to single-cell data. [Argelaguet et al. 2020](<https://link.springer.com/article/10.1186/s13059-020-02015-1> "MOFA+: a statistical framework for comprehensive integration of multi-modal single-cell data; Genome Biol").

## Supervised projections and metrics

- **Multi-view Fisher Discriminant Analysis** - Extends kernel Fisher discrimination to aligned views, with sparse and private-direction variants for supervised classification. [Diethe et al. 2010](<https://link.springer.com/chapter/10.1007/978-3-642-15880-3_27> "Constructing Nonlinear Discriminants from Multiple Data Views; LNCS").
- **Generalized Multiview Analysis** - Learns a discriminative latent space for heterogeneous views using class labels; supports cross-view classification and retrieval with linear and kernel formulations. [Sharma et al. 2012](<https://users.umiacs.umd.edu/~hal3/docs/daume12gma.pdf> "Generalized Multiview Analysis: A discriminative latent space; CVPR").
- **Multiview Metric Learning** - Combines cross-view correspondence with within-view local smoothness; learns mappings into a shared space for previously unseen samples. [Zhai et al. 2012](<https://vipl.ict.ac.cn/publications/earlier/jour/202212/P020221231570717241981.pdf> "Multiview Metric Learning with Global Consistency and Local Smoothness; ACM Trans. Intell. Syst. Technol.").

## Multiple kernel learning

- **MARK** - Builds heterogeneous kernel models through boosting and kernel column generation, selecting basis functions from multiple kernels during learning. [Bennett et al. 2002](<https://doi.org/10.1145/775047.775051> "MARK: a boosting algorithm for heterogeneous kernel models; KDD").
- **SimpleMKL** - Learns a sparse convex combination of kernels jointly with an SVM, alternating classifier optimization and updates of kernel weights. [Rakotomamonjy et al. 2008](<https://jmlr.org/papers/v9/rakotomamonjy08a.html> "SimpleMKL; JMLR").
- **Multiple Kernel Learning Algorithms** - Surveys kernel combination rules and learning objectives. Kernels can encode distinct views, feature subsets, or similarity functions over the same observations. [Gönen and Alpaydin 2011](<https://jmlr.org/papers/v12/gonen11a.html> "Multiple Kernel Learning Algorithms; JMLR").

## Graph fusion and clustering

- **Co-regularized Spectral Clustering** - Couples spectral embeddings of view-specific similarity graphs through agreement penalties, rather than concatenating raw features. [Kumar et al. 2011](<https://proceedings.neurips.cc/paper/2011/hash/31839b036f63806cba3f47b93af8ccb5-Abstract.html> "Co-regularized Multi-view Spectral Clustering; NeurIPS").
- **Multi-view Clustering via Joint NMF** - Factorizes nonnegative views while encouraging their cluster representations toward a common consensus; retains a separate basis for each view. [Liu et al. 2013](<https://www.microsoft.com/en-us/research/wp-content/uploads/2013/05/sdm13multiview.pdf> "Multi-View Clustering via Joint Nonnegative Matrix Factorization; SDM").
- **Similarity Network Fusion** - Constructs a sample-similarity network for each data type and iteratively fuses the networks. Views share sample identities, while their feature sets can differ. [Wang et al. 2014](<https://www.nature.com/articles/nmeth.2810> "Similarity network fusion for aggregating data types on a genomic scale; Nature Methods").

## Missing views

- **Partial Multi-View Clustering** - Learns a common subspace from two partially overlapping views, using paired examples to connect them; neither view must contain every example. [Li et al. 2014](<https://ojs.aaai.org/index.php/AAAI/article/view/8973> "Partial Multi-View Clustering; AAAI").
- **Multimodal VAE** - Uses a product-of-experts inference network and subsampled training to infer shared latent variables from different subsets of modalities; models joint generation and missing-modality inference. [Wu and Goodman 2018](<https://arxiv.org/abs/1802.05335> "Multimodal Generative Models for Scalable Weakly-Supervised Learning; NeurIPS").
- **Mixture-of-experts multimodal VAEs** - Uses a mixture-of-experts variational posterior for multimodal generative learning, aiming to separate shared and modality-specific factors and support joint and cross-modal generation. [Shi et al. 2019](<https://arxiv.org/abs/1911.03393> "Variational Mixture-of-Experts Autoencoders for Multi-Modal Deep Generative Models; NeurIPS").
- **COMPLETER** - Combines contrastive agreement with dual prediction between latent views, recovering missing representations for incomplete multi-view clustering. [Lin et al. 2021](<https://openaccess.thecvf.com/content/CVPR2021/html/Lin_COMPLETER_Incomplete_Multi-View_Clustering_via_Contrastive_Prediction_CVPR_2021_paper.html> "COMPLETER: Incomplete Multi-View Clustering via Contrastive Prediction; CVPR").

## Cross-modal alignment and fusion

- **Tensor Fusion Network** - Forms an outer-product tensor from augmented language, visual and acoustic embeddings, explicitly representing unimodal, pairwise and three-way interactions. [Zadeh et al. 2017](<https://arxiv.org/abs/1707.07250> "Tensor Fusion Network for Multimodal Sentiment Analysis; EMNLP").
- **Gated Multimodal Units** - Learns multiplicative gates that control each modality's contribution to a fused representation; demonstrated with text and images for movie-genre prediction. [Arevalo et al. 2017](<https://arxiv.org/abs/1702.01992> "Gated Multimodal Units for Information Fusion; arXiv").
- **Multimodal Transformer** - Uses directional cross-modal attention to fuse language, audio, and visual sequences without explicit time-step alignment. Modalities still describe the same example. [Tsai et al. 2019](<https://aclanthology.org/P19-1656/> "Multimodal Transformer for Unaligned Multimodal Language Sequences; ACL").
- **Contrastive Multiview Coding** - Contrasts matching views of a scene against mismatched observations, learning representations of shared information across multiple sensory channels. [Tian et al. 2020](<https://arxiv.org/abs/1906.05849> "Contrastive Multiview Coding; ECCV").
- **CLIP** - Trains image and text encoders to identify matching pairs within a batch. Their shared space supports text-image retrieval and classification using text descriptions of classes. [Radford et al. 2021](<https://proceedings.mlr.press/v139/radford21a.html> "Learning Transferable Visual Models From Natural Language Supervision; ICML"); [code](<https://github.com/openai/CLIP>).
- **ImageBind** - Connects six modalities through image-paired training data; alignment does not require training pairs for every pair of modalities. [Girdhar et al. 2023](<https://openaccess.thecvf.com/content/CVPR2023/html/Girdhar_ImageBind_One_Embedding_Space_To_Bind_Them_All_CVPR_2023_paper.html> "ImageBind: One Embedding Space To Bind Them All; CVPR").
- **Multimodal data-mixture scaling** - Fits native text/image/audio MoE losses and checks three held-out training runs; 8 of 9 modality losses are within 2.6%. Transfer is asymmetric in this setup; fitted mixture coefficients depend on tokenizers, data and architecture. [Khandelwal et al. 2026](<https://arxiv.org/abs/2610.14423v1> "Scaling Laws for Multimodal Data Mixtures; NeurIPS").

## Vision-language generation

- **Flamingo** - Connects frozen vision and language backbones through a visual resampler and gated cross-attention. Interleaved image/video-text prompts support few-shot generation; this differs from CLIP-style embedding alignment. [Alayrac et al. 2022](<https://proceedings.neurips.cc/paper_files/paper/2022/hash/960a172bc7fbf0177ccccbb411a7d800-Abstract-Conference.html> "Flamingo: a Visual Language Model for Few-Shot Learning; NeurIPS").
- **Visual instruction tuning** - LLaVA connects a vision encoder to a language model and tunes on image-conditioned instructions generated from captions and boxes. The original open-ended comparison uses GPT-4 judgments; ScienceQA provides a separate task evaluation. [Liu et al. 2023](<https://proceedings.neurips.cc/paper_files/paper/2023/hash/6dcf277ea32ce3288914faf369fe6de0-Abstract-Conference.html> "Visual Instruction Tuning; NeurIPS").

## View selection and evaluation

- **InfoMin** - Studies contrastive view selection: reduce shared information while retaining information needed for the downstream task. Removing task-relevant content violates this principle. [Tian et al. 2020](<https://arxiv.org/abs/2005.10243> "What Makes for Good Views for Contrastive Learning?; NeurIPS").
- **Gradient-Blending** - Finds that joint models can underperform individual modalities on video benchmarks; weights training losses using estimates of overfitting and generalization across modalities. [Wang et al. 2020](<https://openaccess.thecvf.com/content_CVPR_2020/html/Wang_What_Makes_Training_Multi-Modal_Classification_Networks_Hard_CVPR_2020_paper.html> "What Makes Training Multi-Modal Classification Networks Hard?; CVPR").
- **MultiBench** - Benchmarks multimodal prediction across domains, measuring task performance, training/inference cost, and robustness to noisy or missing modalities. [Liang et al. 2021](<https://arxiv.org/abs/2107.07502> "MultiBench: Multiscale Benchmarks for Multimodal Representation Learning; NeurIPS").

## Software

- **mvlearn** - Python implementations for multi-view decomposition, clustering, and semi-supervised learning with a scikit-learn-style API. [Perry et al. 2021](<https://arxiv.org/abs/2005.11890> "mvlearn: Multiview Machine Learning in Python; JMLR"); [code](<https://github.com/mvlearn/mvlearn>).
- **CCA-Zoo** - Linear, regularized, kernel, deep, and probabilistic CCA implementations. Separate multi-view model-selection utilities preserve sample correspondence. [docs](<https://jameschapman19.github.io/cca_zoo/>), [code](<https://github.com/jameschapman19/cca_zoo>).
- **MKLpy** - Python kernel construction, normalization, combination, and evaluation; includes EasyMKL and GRAM. [docs](<https://mklpy.readthedocs.io/en/latest/>).
- **MOFA2 / mofapy2** - R and Python tools for multi-omics factor analysis on the same or overlapping sample sets, including multi-group models and analysis of learned factors. [docs](<https://biofam.github.io/MOFA2/>).
- **MultiBench code** - Data loaders, fusion methods, training routines, and evaluation tools for multimodal prediction benchmarks. [code](<https://github.com/human-ai-lab/multibench>).
- **multiview** - Python multi-view MDS, t-SNE, and spectral clustering. Distinct from mvlearn. [code](<https://pypi.org/project/multiview/>), [code](<https://github.com/mariceli3/multiview>).
- **Multiview-FDA** - MATLAB routines for multi-view Fisher discrimination, citing Diethe et al.'s 2010 work on nonlinear discriminants from multiple data views. [code](<https://github.com/tdiethe/Multiview-FDA>).

## Related topics

- [Feature Extraction](https://mlpapers.org/feature-extraction/)
- [Ensemble Learning](https://mlpapers.org/ensemble-learning/)
- [Missing Data](https://mlpapers.org/missing-data/)
- [Computer Vision](https://mlpapers.org/computer-vision/)
- [NLP](https://mlpapers.org/nlp/)
