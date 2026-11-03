## Reading
### Introduction
- [x] [Learning with not Enough Data Part 1: Semi-Supervised Learning (Lilian Weng, 2021)](https://lilianweng.github.io/posts/2021-12-05-semi-supervised/)
### Papers
- [ ] [A Survey on Semi-Supervised Learning (van Engelen & Hoos, Machine Learning 2020)](https://link.springer.com/article/10.1007/s10994-019-05855-6)
	- classical taxonomy: wrapper methods (self-training, co-training), unsupervised preprocessing, intrinsically semi-supervised, transductive/graph-based
- [x] [A Survey on Deep Semi-supervised Learning (Yang et al., IEEE TKDE 2023; arXiv 2021)](https://arxiv.org/abs/2103.00550)
	- taxonomy: deep generative, consistency regularization, graph-based, pseudo-labeling, hybrid; arXiv abstract reviews 52 representative methods (TKDE version says 60)
- [ ] [Semi-Supervised and Unsupervised Deep Visual Learning: A Survey (Chen et al., 2022)](https://arxiv.org/abs/2208.11296)
- [ ] [Revisiting Semi-Supervised Learning in the Era of Foundation Models (Zhang et al., 2025)](https://arxiv.org/abs/2503.09707)
	- finds parameter-efficient fine-tuning (PEFT) on labeled data alone often matches SSL; proposes ensembling multiple PEFT approaches and VFM backbones for more robust self-training pseudo-labels
- [ ] [Awesome Semi-Supervised Learning GitHub](https://github.com/yassouali/awesome-semi-supervised-learning)

## Benchmark(s)
- [USB: A Unified Semi-supervised Learning Benchmark for Classification (NeurIPS 2022 Datasets & Benchmarks)](https://arxiv.org/abs/2208.07204)
	- 15 tasks across CV, NLP, and Audio (5 datasets each); on a single V100, 39 GPU days to evaluate FixMatch on all 15 USB tasks vs 335 GPU days on 5 CV tasks with TorchSSL
- [Realistic Evaluation of Deep Semi-Supervised Learning Algorithms (Oliver et al., NeurIPS 2018)](https://arxiv.org/abs/1804.09170)
	- [Code](https://github.com/brain-research/realistic-ssl-evaluation)

## Advancements
- Consistency regularization
	- [Temporal Ensembling for Semi-Supervised Learning (Π-Model & Temporal Ensembling, ICLR 2017)](https://arxiv.org/abs/1610.02242)
	- [Mean Teachers are Better Role Models (Mean Teacher, NeurIPS 2017)](https://arxiv.org/abs/1703.01780) 
	- [Virtual Adversarial Training (VAT, IEEE TPAMI)](https://arxiv.org/abs/1704.03976) 
	- [Unsupervised Data Augmentation for Consistency Training (UDA, NeurIPS 2020)](https://arxiv.org/abs/1904.12848) 
- Pseudo-labeling / self-training
	- [Pseudo-Label: The Simple and Efficient Semi-Supervised Learning Method for Deep Neural Networks (Lee, ICML 2013 Workshop)](https://www.semanticscholar.org/paper/Pseudo-Label-:-The-Simple-and-Efficient-Learning-Lee/798d9840d2439a0e5d47bcf5d164aa46d5e7dc26) 
	- [Self-training with Noisy Student improves ImageNet classification (CVPR 2020)](https://arxiv.org/abs/1911.04252) 
	- [Meta Pseudo Labels (CVPR 2021)](https://arxiv.org/abs/2003.10580) 
- Hybrid / holistic
	- [MixMatch: A Holistic Approach to Semi-Supervised Learning (NeurIPS 2019)](https://arxiv.org/abs/1905.02249) 
	- [ReMixMatch: Distribution Alignment and Augmentation Anchoring (ICLR 2020)](https://arxiv.org/abs/1911.09785)
	- [FixMatch: Simplifying Semi-Supervised Learning with Consistency and Confidence (NeurIPS 2020)](https://arxiv.org/abs/2001.07685) 
- Adaptive thresholding
	- [FlexMatch: Curriculum Pseudo Labeling (NeurIPS 2021)](https://arxiv.org/abs/2110.08263)
	- [FreeMatch: Self-adaptive Thresholding (ICLR 2023)](https://arxiv.org/abs/2205.07246) 
	- [SoftMatch: Addressing the Quantity-Quality Trade-off (ICLR 2023)](https://arxiv.org/abs/2301.10921)
- Graph-based
	- [Label Propagation for Deep Semi-supervised Learning (Iscen et al., CVPR 2019)](https://arxiv.org/abs/1904.04717) 
- SSL for NLP / LLMs
	- [Rethinking Semi-supervised Learning with Language Models (2023)](https://arxiv.org/abs/2305.13002)
		- vs five state-of-the-art self-training approaches, task-adaptive pre-training (TAPT) is a stronger, more robust SSL learner, even with a few hundred unlabeled samples or under domain shift
	- [Want To Reduce Labeling Cost? GPT-3 Can Help (2021)](https://arxiv.org/abs/2108.13487)
		- LLM-as-labeler: GPT-3 labels cost 50–96% less than human labels for the same downstream performance; combines GPT-3 pseudo-labels with human labels

## Tutorials
- [ ] [scikit-learn User Guide: Semi-supervised learning](https://scikit-learn.org/stable/modules/semi_supervised.html)
	- SelfTrainingClassifier, LabelPropagation, LabelSpreading
- [ ] [scikit-learn: Semi-supervised Classification on a Text Dataset](https://scikit-learn.org/stable/auto_examples/semi_supervised/plot_semi_supervised_newsgroups.html)
	- compares self-training vs LabelSpreading with 20% labels
- [ ] [PyTorch Tutorial: Semi-Supervised Learning using USB](https://docs.pytorch.org/tutorials/advanced/usb_semisup_learn.html)
	- trains FreeMatch/SoftMatch on CIFAR-10 with 40 labels using a pretrained ViT 

## Tools
- [USB (microsoft/Semi-supervised-learning)](https://github.com/microsoft/Semi-supervised-learning)
	- [ ] [Paper](https://arxiv.org/abs/2208.07204)
	- [Docs](https://usb.readthedocs.io/) · `pip install semilearn`
- [scikit-learn semi_supervised](https://scikit-learn.org/stable/api/sklearn.semi_supervised.html)
	- [ ] [Paper (Zhu & Ghahramani 2002, Label Propagation)](http://reports-archive.adm.cs.cmu.edu/anon/cald/abstracts/02-107.html)
- [FixMatch (google-research/fixmatch)](https://github.com/google-research/fixmatch) 
	- [ ] [Paper](https://arxiv.org/abs/2001.07685)
- [MixMatch (google-research/mixmatch)](https://github.com/google-research/mixmatch) 
	- [ ] [Paper](https://arxiv.org/abs/1905.02249)
- [Noisy Student (google-research/noisystudent)](https://github.com/google-research/noisystudent) 
	- [ ] [Paper](https://arxiv.org/abs/1911.04252)

## Notes
- Popular methods:
	1. Consistency regularization: Image classification
	2. Self-training: Text classification (high dimensional data), speed, scaling,
	3. Label Propagation: small labeled dataset that is 100% correct
	4. Label Spreading: human annotated data that may contain errors
- Self-training:
	- 
- Label Propagation algorithm:
	- [Youtube](https://www.youtube.com/watch?v=Gkk5zx9hA_k)
	- [Medium](https://medium.com/@amit25173/label-propagation-algorithms-in-semi-supervised-learning-bb9d53ae1a60)
	1. Start with a dense or sparse graph (almost always sparse)
		- Encoded as a transition matrix (stochastic matrix)
	2. Random walk from a starting node
	3. For each node, assign its label to be most commonly occurring label of its neighbors
- Label Spreading algorithm:
	- Refined version of the Label Propagation Algorithm, but with a normalized transition matrix
	- Uses soft-clamping (0 < $\alpha$ < 1): determines how much a node adopts its neighbors' labels vs retaining its own. Makes it more robust to outliers
### Learning with not Enough Data Part 1: Semi-Supervised Learning
- Semi-supervised learning trains on labeled and unlabeled data togethe.
- SSL relies on four assumptions: smoothness, cluster, low-density separation, and manifold.
- **Consistency regularization** trains the model to give the same prediction under dropout, augmentation, or other noise.
    - Π-Model → Temporal Ensembling → Mean Teacher: each makes the consistency target cheaper and more stable (two passes → EMA of predictions → EMA of weights).
    - VAT, ICT, and UDA use adversarial noise, MixUp, and strong augmentation, respectively.
- **Pseudo-labeling** (a type of self-training) uses the model's confident predictions as labels, which acts like entropy minimization and pushes decision boundaries into low-density regions (e.g., Noisy Student).
- The main risk is confirmation bias, where the student overfits to the teacher's wrong pseudo labels; Meta Pseudo Labels addresses this by updating the teacher based on how well the student performs.
- Hybrid methods combine both ideas.
    - MixMatch/ReMixMatch: average predictions over several augmentations, sharpen them, then apply MixUp.
    - FixMatch: a confident pseudo label from a weakly augmented view becomes the target for a strongly augmented view of the same sample.
- SSL stacks with pre-training: pre-train a large model, fine-tune it on the few labels, then distill it using unlabeled data.

### A Survey on Deep Semi-supervised Learning (2023)
#### Method families
- Deep generative: (e.g., semi-supervised VAEs/GANs)
- Consistency regularization: [Π-Model/Temporal Ensembling](https://arxiv.org/abs/1610.02242), [Mean Teacher](https://arxiv.org/abs/1703.01780), [VAT](https://arxiv.org/abs/1704.03976), [UDA](https://arxiv.org/abs/1904.12848)
- Graph-based: [Label Propagation (Zhu & Ghahramani 2002)](http://reports-archive.adm.cs.cmu.edu/anon/cald/abstracts/02-107.html), [Label Propagation for Deep SSL](https://arxiv.org/abs/1904.04717)
- Pseudo-labeling: [Pseudo-Label](https://www.semanticscholar.org/paper/Pseudo-Label-:-The-Simple-and-Efficient-Learning-Lee/798d9840d2439a0e5d47bcf5d164aa46d5e7dc26), [Noisy Student](https://arxiv.org/abs/1911.04252), [Meta Pseudo Labels](https://arxiv.org/abs/2003.10580)
- Hybrid: [MixMatch](https://arxiv.org/abs/1905.02249), [ReMixMatch](https://arxiv.org/abs/1911.09785), [FixMatch](https://arxiv.org/abs/2001.07685) → adaptive thresholds: [FlexMatch](https://arxiv.org/abs/2110.08263), [FreeMatch](https://arxiv.org/abs/2205.07246), [SoftMatch](https://arxiv.org/abs/2301.10921)


### Revisiting Semi-Supervised Learning in the Era of Foundation Models
- Asks whether classic SSL methods still help when you start from a pretrained vision foundation model (VFM) like CLIP or DINOv2 instead of training from scratch.
- Builds a new benchmark from six VTAB datasets (textures, scenes, remote sensing, medical, counting, driving), because frozen VFMs already nearly solve CIFAR-type datasets.
- Tunes hyperparameters without labels by ranking configurations across seven unsupervised clustering/confidence metrics on a held-out _unlabeled_ set, which avoids leaking labeled validation data.
- Under fair tuning, fine-tuning on the labeled data alone matches or beats FixMatch, FlexMatch, SoftMatch, and FineSSL.
- Parameter-efficient fine-tuning (LoRA, AdaptFormer) improves both SSL and labeled-only training, but the gap between them stays small, so current SSL methods barely use the unlabeled data.
- Proposes V-PET, a simple self-training baseline:
    - Fine-tune several VFM + PEFT pairs on the labeled data only.
    - Have each pair predict a one-hot label for every unlabeled sample, then average those one-hot votes into a soft label ("Mean Labels"). This works better than averaging logits or probabilities, which have inconsistent scales across models.
    - Train one model on all the pseudo-labels in a single round, with no confidence threshold.
- Diversity is what makes the ensemble work: gains grow from self-training → PET (ensemble over PEFT methods) → V-PET (ensemble over PEFT methods and VFMs), with diminishing returns beyond about 2–4 sources.
### USB: A Unified Semi-supervised Learning Benchmark
- Argues that SSL benchmarks are too narrow (CV only) and too expensive (training ResNets from scratch).
- Proposes 15 tasks across CV, NLP, and audio, using pretrained backbones (ViT, BERT, Wav2Vec 2.0/HuBERT).
    - Evaluating FixMatch costs about 39 GPU-days in USB versus about 335 in TorchSSL.
- Implements 14 SSL algorithms in one modular codebase (`pip install semilearn`), with each algorithm broken into components such as pseudo-labeling, thresholding, distribution alignment, and weak/strong augmentation.
- Algorithm rankings change across domains, so an SSL method should be tested on more than vision.
    - **ReMixMatch ranks first on CV, SimMatch on NLP, AdaMatch on audio**.
    - Adaptive-threshold methods (FlexMatch, AdaMatch) are consistently strong.
- Pretraining speeds up SSL and improves results; several older methods that barely converge from scratch work fine on a pretrained ViT.
- **SSL can do _worse_ than supervised training when labels are very scarce**, especially for older methods on NLP and audio. CRMatch, AdaMatch, and SimMatch were the most robust.
- MixMatch and ReMixMatch were skipped for NLP and audio because mixing inputs of different lengths hurt performance.
### Realistic Evaluation of Deep Semi-Supervised Learning Algorithms
- Argues that standard SSL evaluation (drop most labels from CIFAR-10 or SVHN) overstates real-world gains, and reimplements Π-Model, Mean Teacher, VAT, entropy minimization, and Pseudo-Label on one shared WRN-28-2 model.
- With equal tuning effort for the supervised baseline (1000 trials each), the gap between SSL and labeled-only training shrinks a lot.
    - Π-Model: 20.3% → 16.4% error here, versus 34.9% → 12.4% as originally reported.
- **Transfer learning from ImageNet beat every SSL method on CIFAR-10 (12.1% error), making it a frequently omitted but strong baseline.**
- Unlabeled data from classes not in the labeled set (class distribution mismatch) can make performance _worse_ than using no unlabeled data at all.
- Methods differ in how sensitive they are to the amount of labeled and unlabeled data, and gains plateaued at about 80k unlabeled examples on SVHN.
- Realistically small validation sets are too noisy to tell methods apart; by Hoeffding's bound, measuring error to ±1% with 95% confidence needs about 20k examples.
- Recommendations: use the same model for all methods, report strong supervised and transfer baselines, vary class mismatch and data amounts, and don't over-tune on large validation sets.
### Rethinking Semi-supervised Learning with Language Models
- Compares two ways to use unlabeled text with RoBERTa:
    - Self-training (ST): five methods (VAT, FixMatch, Dash, FlexMatch, AdaMatch) that train on pseudo-labels.
    - Task-adaptive pretraining (TAPT): continue masked-language-model pretraining on the task's unlabeled text, then fine-tune on the labels.
- **TAPT matches or beats the ST methods on several datasets** (best on Amazon Review and Yahoo! Answers) with lower variance, so it should be a standard SSL baseline in NLP.
- TAPT helps even with only 100–1,000 unlabeled samples, and its gain over plain fine-tuning grows as labels become scarcer.
- ST is fragile at the extremes:
    - With too few labels, it collapses (often to near-random) regardless of how much unlabeled data there is, likely from confirmation bias.
    - With too little unlabeled data, it often falls below the supervised baseline (33–67% of runs), while TAPT never did.
- Under domain shift between labeled and unlabeled data, ST can drop to random-guess level, while TAPT stays stable and sometimes even benefits.
- Starting ST from a TAPT checkpoint helps slightly but doesn't fix these failure modes.
- The authors suggest future SSL work rely more on unsupervised pretraining objectives than on pseudo-labels.
### Self-training with Noisy Student improves ImageNet classification
- Noisy Student is self-training with two changes:
    - The student is equal to or larger than the teacher.
    - The student is trained with noise, while the teacher labels clean inputs without noise.
- **Algorithm**:
    1. Train a teacher on the labeled data.
    2. The un-noised teacher pseudo-labels the unlabeled data (soft or hard labels).
    3. Train a noised student on both the labeled and pseudo-labeled data together.
    4. Make the student the new teacher and repeat. Their best model used 3 iterations.
- Noise comes in two types:
    - Input noise: RandAugment.
    - Model noise: dropout and stochastic depth.
- The noise is why the student can surpass the teacher: it has to match a clean teacher on augmented inputs, and it has to imitate a teacher that acts like an ensemble when dropout is off. Removing the noise, or noising the teacher instead, lowers accuracy.
- Unlabeled data is filtered and balanced:
    - Drop low-confidence images, which are usually out-of-domain.
    - Cap each class at the most confident images, and duplicate images in underrepresented classes. This helps small models most.
- Results:
    - 88.4% ImageNet top-1, beating the prior best (which used 3.5B weakly labeled Instagram images) with only 300M unlabeled images.
    - Large robustness gains it wasn't trained for, e.g. ImageNet-A accuracy rose from 61.0% to 83.7%.
- Practical takeaways from the ablations:
    - A better teacher, a larger student, and more unlabeled data all help.
    - Soft pseudo-labels are safer than hard ones for out-of-domain data.
    - Joint training on labeled and pseudo-labeled data beats pretraining on pseudo-labels and then fine-tuning.
- Consistency-regularization and pseudo-labeling methods worked worse at ImageNet scale. They generate targets from the model still being trained, which is inaccurate early on, whereas Noisy Student uses a separate teacher that is already fully trained.