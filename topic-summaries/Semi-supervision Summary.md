## Key Findings
- A well-tuned labeled-only baseline (supervised training, transfer learning, or PEFT on a pretrained model) often closes most of the gap that SSL papers report.
	- The Evolution into Self-Supervised Pretraining
- Pretraining often matters more than the choice of SSL algorithm: TAPT in NLP and foundation models in vision deliver most of the gains.
	- Fine-tuning on small labeled subset
	- Google's *Noisy Student*
- Self-training is fragile because of confirmation bias, and it can collapse when there are too few labels or too little unlabeled data.
- Label Propagation and Label Spreading are two popular forms of SSL but Label Propagation is largely obsolete
- When the unlabeled data comes from different classes or domains than the labeled data, SSL can perform worse than using no unlabeled data at all.
- Algorithm rankings change across CV, NLP, and audio, so results on vision benchmarks don't reliably transfer to text.

## Diagram(s)

![[semi_supervised_learning.png]]

![[Label Propagation vs. Label Spreading@1x.png]]
## Recent Advancements
- Adaptive thresholding (FlexMatch, FreeMatch, SoftMatch) replaces FixMatch's fixed confidence cutoff with class-wise or self-adjusting thresholds to balance pseudo-label quality and quantity.
- Starting SSL from pretrained backbones (as in USB) cuts compute from about 335 to about 39 GPU-days and helps older methods converge.
- V-PET combines parameter-efficient fine-tuning with one-hot "Mean Labels" ensembling across models to get robust pseudo-labels in a single round of self-training.
- Hyperparameters can now be tuned without labels by ranking configurations on unsupervised clustering metrics computed on a held-out unlabeled set.
- In NLP, the field is moving from pseudo-labels toward unsupervised pretraining objectives like TAPT as the main way to use unlabeled text.
## Current Best Approaches (Benchmarks)
- On USB's NLP tasks, SimMatch ranks first, followed by CRMatch and CoMatch.
- Adaptive-threshold methods like FlexMatch and AdaMatch are consistently strong across CV, NLP, and audio.
- CRMatch, AdaMatch, and SimMatch are the most robust, rarely falling below the supervised baseline.
- For text, TAPT followed by fine-tuning matches or beats the five self-training methods it was tested against, with lower variance.
- With foundation-model backbones, V-PET's ensembled pseudo-labels outperform FixMatch, FlexMatch, SoftMatch, and FineSSL.
- For classical graph methods, Label Propagation suits small, fully correct labeled sets, while Label Spreading's soft clamping handles noisy human labels better.