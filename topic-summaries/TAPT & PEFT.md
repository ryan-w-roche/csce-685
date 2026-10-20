## Key Findings
#### TAPT
- Continued masked-word pretraining still helps strong pretrained models (RoBERTa)
- DAPT gains largest for domains far from the original training text (biomedical, CS)
- TAPT: cheap (~60× faster than DAPT), beat the baseline on all 8 tasks, often matched DAPT
- **DAPT → TAPT best on every task**
- Pretraining on an irrelevant domain hurts; relevance beats volume
- TAPT is task-specific; no transfer to other tasks in the same domain
- More unlabeled text from the task’s own distribution → bigger gains
- Conventional TAPT unreliable for sentence-pair tasks and prompt-based fine-tuning
- Gains possible with only hundreds to ~1K unlabeled examples

#### PEFT
- Freeze the base model, train <1–4% of parameters → near full fine-tuning quality
- Adapters: within 0.4 pts of full fine-tuning on GLUE with 3.6% params, but 20–30% slower inference at batch size 1
- LoRA: low-rank weight updates merged into the model → zero added inference cost
- Weight updates have very low intrinsic rank; r = 1–8 often enough
- Same budget: more adapted matrices at low rank > one matrix at high rank
- LoRA amplifies features the model already has but underuses
- **LoRA strong with little data** (100 examples: 63.8 vs. 60.2 for full fine-tuning)
- QLoRA: 4-bit base + LoRA matches 16-bit quality; 65B model on one 48GB GPU
- LoRA on all linear layers is critical; rank barely matters after that
- Fine-tuning data quality > dataset size


## Diagram(s)
#### TAPT:
![[pcp.png]]

#### PEFT:
Adapters:
![[Pasted image 20261019132136.png]]

LoRA:
![[Pasted image 20261019132233.png]]

## Current Best Approaches (Benchmarks)
#### TAPT
- DAPT → TAPT: best accuracy when a large domain corpus exists
- TAPT alone: best cost/benefit default for classification
- Curated-TAPT: ~95% of fully supervised DAPT + TAPT using 0.3% of labels (RCT-500)
- kNN-TAPT when no extra task text exists; approaches DAPT as neighbors increase
- PCP for prompt-based fine-tuning with few labels:
    - +6.8 pts average in the semi-supervised setting
    - Beat FixMatch, Dash, FlexMatch and AdaMatch on 4 of 5 benchmarks
- LLM continued pretraining: LR re-warming + re-decaying + replay of old data ≈ full retraining at a fraction of the compute
- Large new-knowledge injection: full-parameter CPT > LoRA CPT

#### PEFT
- LoRA: default choice; top score on PEFT-Bench (27 datasets, 7 methods)
- QLoRA: default when GPU memory is tight
- BitFit / LayerNorm-tuning: cheapest; match LoRA on MNLI, SST-2, RTE, MMLU
- LoRA settings:
    - All layers (MLP layers matter most)
    - Learning rate ~10× higher than full fine-tuning
    - α ≈ 2r
    - Avoid very large batches
- LoRA ≈ full fine-tuning for instruction tuning; lags for large-scale continued pretraining
- Claimed LoRA-beaters struggle with limited hyperparameter tuning
- Vision: VTAB-1k and V-PEFT Bench are standard; SSF beats full fine-tuning on VTAB-1k (73.1 vs. 65.6)

## Recent Advancements
#### TAPT

- PCP (NeurIPS 2023): prompt templates + pseudo-labels inside continued pretraining
- AdaptLLM (ICLR 2024): domain text rewritten as reading-comprehension tasks; 7B competitive with BloombergGPT-50B
- Continual-pretraining recipes for LLMs (TMLR 2024): re-warm, re-decay, replay
- LoRA Learns Less and Forgets Less (TMLR 2024): LoRA weak for continued pretraining but forgets less
- Continual learning survey (ACM CSUR 2025): continued pretraining → domain-adaptive pretraining → continual fine-tuning pipeline
- Open directions: TAPT/PCP combined with PEFT; decoder-only LLMs

#### PEFT

- DoRA (ICML 2024): magnitude + direction split; beats LoRA at no extra inference cost
- LoRA+ (ICML 2024): separate learning rates for A and B; up to ~2× faster
- PiSSA (NeurIPS 2024): initialized from the model’s top singular directions (SVD); ~5 pts over LoRA on GSM8K
- VeRA (ICLR 2024): shared random matrices; even fewer trainable params
- LoRA Without Regret (2025): when and how LoRA matches full fine-tuning
- PEFT-Bench / PEFT-Factory (2025): end-to-end benchmarking incl. speed and memory
- Tooling: HF PEFT, Unsloth (fast single-GPU QLoRA)