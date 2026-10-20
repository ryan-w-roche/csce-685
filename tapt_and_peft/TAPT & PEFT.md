## Reading

### Introduction

- [ ] [Parameter-Efficient LLM Finetuning With Low-Rank Adaptation (LoRA) (Sebastian Raschka, 2023)](https://sebastianraschka.com/blog/2023/llm-finetuning-lora.html)

### Papers

- [ ] [Parameter-Efficient Fine-Tuning of Large-Scale Pre-Trained Language Models — "Delta Tuning" (Ding et al., Nature Machine Intelligence 2023)](https://www.nature.com/articles/s42256-023-00626-4)
    - Splits PEFT into addition-, specification- and reparameterization-based "delta tuning"; gives optimization/optimal-control theory; shows that the gaps between methods shrink as model scale grows
- [ ] [Parameter-Efficient Fine-Tuning for Large Models: A Comprehensive Survey (Han, Gao, Liu, Zhang & Zhang, arXiv 2024)](https://arxiv.org/abs/2403.14608)
    - Taxonomy: additive, selective, reparameterized and hybrid PEFT, plus a section on efficient PEFT system design (serving and distributed training); covers LLMs, ViTs, diffusion models and VLMs
- [ ] [Scaling Down to Scale Up: A Guide to Parameter-Efficient Fine-Tuning (Lialin, Deshpande, Yao & Rumshisky, arXiv 2023/2024)](https://arxiv.org/abs/2303.15647)
    - Covers 50+ papers (2019–mid-2024); head-to-head comparison of 15 PEFT methods on models up to 11B; methods reported to beat LoRA struggle when hyperparameter tuning is limited
- [ ] [Parameter-Efficient Fine-Tuning for Pre-Trained Vision Models: A Survey and Benchmark (Xin et al., arXiv 2024, submitted to IJCV)](https://arxiv.org/abs/2402.02242)
    - Visual PEFT taxonomy: addition-based, partial-based, unified-based and multi-task tuning; introduces the V-PEFT Bench (see below)
- [ ] [Continual Learning of Large Language Models: A Comprehensive Survey (Shi et al., ACM Computing Surveys 2025)](https://arxiv.org/abs/2404.16789)
    - "Vertical continuity" pipeline: Continual Pre-Training (CPT) → Domain-Adaptive Pre-training (DAP) → Continual Fine-Tuning (CFT); also covers horizontal continuity across time and domains
- [ ] [Awesome-Parameter-Efficient-Transfer-Learning (synbol, GitHub)](https://github.com/synbol/Awesome-Parameter-Efficient-Transfer-Learning)
    - Companion list to the Xin et al. visual PEFT survey; see also [THUDM/Awesome-Parameter-Efficient-Fine-Tuning-for-Foundation-Models](https://github.com/THUDM/Awesome-Parameter-Efficient-Fine-Tuning-for-Foundation-Models), organized into selective/additive/prompt/reparameterization/hybrid

## Benchmark(s)

- [V-PEFT Bench — in "PEFT for Pre-Trained Vision Models: A Survey and Benchmark" (arXiv 2024)](https://arxiv.org/abs/2402.02242)
    - 2 conventional + 25 PEFT methods across 24 image-recognition datasets, 3 video action-recognition datasets and 3 dense-prediction tasks; proposes a Performance-Parameter Trade-off (PPT) metric
    - [Code](https://github.com/synbol/Parameter-Efficient-Transfer-Learning-Benchmark)
- [PEFT-Bench: A Parameter-Efficient Fine-Tuning Methods Benchmark (Belanec et al., arXiv 2025)](https://arxiv.org/abs/2511.21285)
    - End-to-end benchmark for autoregressive LLMs: 27 NLP datasets, 7 PEFT methods; PSCP metric penalizes trainable params, inference speed and training memory; LoRA scores highest, while BitFit/LNTuning are more efficient and match it on MNLI, SST-2, RTE and MMLU
    - [Framework: PEFT-Factory](https://arxiv.org/abs/2512.02764)
- [VTAB: A Large-scale Study of Representation Learning with the Visual Task Adaptation Benchmark (Zhai et al., arXiv 2019)](https://arxiv.org/abs/1910.04867)
    - VTAB-1k: 19 tasks (Natural / Specialized / Structured) with 1,000 labelled examples each (800 train / 200 val); the de facto benchmark for visual PEFT (VPT, AdaptFormer, SSF)

## Advancements

- Adapters / Additive methods
    - [Parameter-Efficient Transfer Learning for NLP (Adapters, ICML 2019)](https://arxiv.org/abs/1902.00751)
        - Bottleneck adapters reach within 0.4% of full fine-tuning on GLUE while adding 3.6% parameters per task
    - [AdapterFusion: Non-Destructive Task Composition for Transfer Learning (AdapterFusion, EACL 2021)](https://arxiv.org/abs/2005.00247)
    - [Compacter: Efficient Low-Rank Hypercomplex Adapter Layers (Compacter, NeurIPS 2021)](https://arxiv.org/abs/2106.04647)
        - Trains 0.047% of parameters and matches full fine-tuning on GLUE
    - [LLM-Adapters: An Adapter Family for Parameter-Efficient Fine-Tuning of Large Language Models (LLM-Adapters, EMNLP 2023)](https://arxiv.org/abs/2304.01933)
        - Series/parallel adapters, prompt-based methods and LoRA evaluated on 14 arithmetic and commonsense datasets; releases Math10K and Commonsense170K, now standard LoRA-variant eval sets
- Prompt / Prefix tuning
    - [Prefix-Tuning: Optimizing Continuous Prompts for Generation (Prefix-Tuning, ACL 2021)](https://arxiv.org/abs/2101.00190)
        - Tunes 0.1% of parameters
    - [The Power of Scale for Parameter-Efficient Prompt Tuning (Prompt Tuning, EMNLP 2021)](https://arxiv.org/abs/2104.08691)
        - In T5 ablations, prompt tuning "closes the gap" and matches full model tuning once models exceed billions of parameters
    - [P-Tuning v2: Prompt Tuning Can Be Comparable to Fine-tuning Universally Across Scales and Tasks (P-Tuning v2, ACL 2022)](https://arxiv.org/abs/2110.07602)
        - Deep prompts at every layer match fine-tuning with 0.1%–3% tuned params
- Reparameterization / Low-rank: LoRA and variants
    - [LoRA: Low-Rank Adaptation of Large Language Models (LoRA, ICLR 2022)](https://arxiv.org/abs/2106.09685)
        - 10,000× fewer trainable params and 3× less GPU memory than full fine-tuning of GPT-3 175B; mergeable, so zero extra inference latency
    - [QLoRA: Efficient Finetuning of Quantized LLMs (QLoRA, NeurIPS 2023)](https://arxiv.org/abs/2305.14314)
        - 4-bit NF4 + double quantization + paged optimizers; fine-tunes a 65B model on a single 48GB GPU; Guanaco reaches 99.3% of ChatGPT on Vicuna
    - [Adaptive Budget Allocation for Parameter-Efficient Fine-Tuning (AdaLoRA, ICLR 2023)](https://arxiv.org/abs/2303.10512)
    - [VeRA: Vector-based Random Matrix Adaptation (VeRA, ICLR 2024)](https://arxiv.org/abs/2310.11454)
    - [DoRA: Weight-Decomposed Low-Rank Adaptation (DoRA, ICML 2024 Oral)](https://arxiv.org/abs/2402.09353)
        - Decomposes weights into magnitude + direction (LoRA on direction); beats LoRA on LLaMA, LLaVA and VL-BART at no extra inference cost; Oral acceptance rate 1.5%
    - [LoRA+: Efficient Low Rank Adaptation of Large Models (LoRA+, ICML 2024)](https://arxiv.org/abs/2402.12354)
        - Different learning rates for A and B: 1–2% better and up to ~2× faster than LoRA at the same compute cost
    - [PiSSA: Principal Singular Values and Singular Vectors Adaptation of Large Language Models (PiSSA, NeurIPS 2024)](https://arxiv.org/abs/2404.02948)
        - SVD-based init: Mistral-7B GSM8K 72.86% vs LoRA 67.7%; QPiSSA on LLaMA-3-70B 86.05% vs QLoRA 81.73%
- Selective / Rescaling methods
    - [BitFit: Simple Parameter-efficient Fine-tuning for Transformer-based Masked Language-models (BitFit, ACL 2022)](https://arxiv.org/abs/2106.10199)
        - Tunes only bias terms; competitive with full fine-tuning on BERT for small-to-medium data
    - [Few-Shot Parameter-Efficient Fine-Tuning is Better and Cheaper than In-Context Learning ((IA)³ / T-Few, NeurIPS 2022)](https://arxiv.org/abs/2205.05638)
        - Learned vectors rescale activations; T-Few is the first to reach super-human performance on RAFT, beating the prior best by 6% absolute
- Unified / Hybrid views & scaling analyses
    - [Towards a Unified View of Parameter-Efficient Transfer Learning (He et al., ICLR 2022)](https://arxiv.org/abs/2110.04366)
        - Recasts adapters, prefix tuning and LoRA as modifications to hidden states; motivates hybrid "Mix-and-Match" adapters
    - [LoRA Learns Less and Forgets Less (Biderman et al., TMLR 2024)](https://arxiv.org/abs/2405.09673)
        - Code/math with approximately 100K instruction-finetuning prompt-response pairs and 20B unstructured CPT tokens; in standard low-rank settings LoRA substantially underperforms full fine-tuning (especially in CPT) but forgets less; full fine-tuning learns perturbations with 10–100× higher rank than typical LoRA configs
- Task / Domain-adaptive pretraining (DAPT/TAPT) & continued pretraining
    - [Don't Stop Pretraining: Adapt Language Models to Domains and Tasks (DAPT/TAPT, ACL 2020)](https://arxiv.org/abs/2004.10964)
        - 4 domains (biomed, CS, news, reviews) × 8 classification tasks; DAPT and TAPT both help, DAPT→TAPT does best on all tasks, and TAPT on augmented task data is a cheap alternative
    - [Don't Stop Pretraining? Make Prompt-based Fine-tuning Powerful Learner (PCP, NeurIPS 2023)](https://arxiv.org/abs/2305.01711)
        - Conventional TAPT can hurt sentence-pair tasks and prompt-based FT; Prompt-based Continued Pre-training improves results by up to 20.1% absolute across 21 benchmarks, in both semi-supervised and fully supervised settings
    - [Simple and Scalable Strategies to Continually Pre-train Large Language Models (Ibrahim et al., TMLR 2024)](https://arxiv.org/abs/2403.08763)
        - LR re-warming + re-decaying + replay of old data matches full re-training with a fraction of the compute: at 405M on English→English and English→German shifts of hundreds of billions of tokens, and for a 10B-parameter LLM
- PEFT for vision foundation models
    - [Visual Prompt Tuning (VPT, ECCV 2022)](https://arxiv.org/abs/2203.12119)
        - Fewer than 1% of parameters trainable; outperforms full fine-tuning in many cases across model capacities and training-data scales
    - [AdaptFormer: Adapting Vision Transformers for Scalable Visual Recognition (AdaptFormer, NeurIPS 2022)](https://arxiv.org/abs/2205.13535)
        - Under 2% extra params; with 1.5% params, about 10% and 19% relative gains over full fine-tuning on SSv2 and HMDB51
    - [Scaling & Shifting Your Features: A New Baseline for Efficient Model Tuning (SSF, NeurIPS 2022)](https://arxiv.org/abs/2210.08823)
        - About 0.3M tuned params; VTAB-1k 73.10 vs 65.57 for full fine-tuning (+11.48%); FGVC 90.72 vs 88.54 (+2.46%)

## Tutorials

- [ ] [Hugging Face PEFT — Quicktour](https://huggingface.co/docs/peft/quicktour)
    - `LoraConfig` + `get_peft_model`, printing trainable-param %, saving and loading adapters
- [ ] [Fine-tuning a masked language model — Hugging Face LLM Course, Ch. 7](https://huggingface.co/learn/llm-course/en/chapter7/3)
    - Hands-on DAPT/TAPT: continues MLM pretraining of DistilBERT on IMDb (domain adaptation) and tracks perplexity, then fine-tunes the classifier
- [ ] [Practical Tips for Finetuning LLMs Using LoRA (Sebastian Raschka, 2023)](https://magazine.sebastianraschka.com/p/practical-tips-for-finetuning-llms)
    - Lessons from hundreds of runs: QLoRA saves 33% memory at the cost of 39% more runtime (14.18 GB / 2.79 h vs 21.33 GB / 1.85 h); apply LoRA to all layers; α ≈ 2r rule of thumb; multi-epoch IFT can hurt
- [ ] [LoRA Without Regret (John Schulman & Thinking Machines Lab, 2025)](https://thinkingmachines.ai/blog/lora/)
    - LoRA matches full fine-tuning in the "low-regret" post-training regime: LoRA on all layers (MLP matters most), optimal LR ~10× higher, LoRA less tolerant of large batches; reproduction guide in [TRL docs](https://huggingface.co/docs/trl/en/lora_without_regret)

## Tools

- [PEFT (huggingface/peft)](https://github.com/huggingface/peft)
    - [Docs](https://huggingface.co/docs/peft) · `pip install peft`
- [LoRA / loralib (microsoft/LoRA)](https://github.com/microsoft/LoRA)
    - [ ] [Paper](https://arxiv.org/abs/2106.09685)
    - `pip install loralib`
- [Adapters (adapter-hub/adapters)](https://github.com/adapter-hub/adapters)
    - [ ] [Paper](https://arxiv.org/abs/2311.11077)
    - [Docs](https://docs.adapterhub.ml/) · `pip install adapters`
- [Don't Stop Pretraining (allenai/dont-stop-pretraining)](https://github.com/allenai/dont-stop-pretraining)
    - [ ] [Paper](https://arxiv.org/abs/2004.10964)
- [QLoRA (artidoro/qlora)](https://github.com/artidoro/qlora)
    - [ ] [Paper](https://arxiv.org/abs/2305.14314)
    - `pip install bitsandbytes peft`
- [Unsloth (unslothai/unsloth)](https://github.com/unslothai/unsloth)
    - [Docs](https://docs.unsloth.ai/) · `pip install unsloth`

## Notes

### TAPT
#### Don't Stop Pretraining: Adapt Language Models to Domains and Tasks (DAPT/TAPT)
- Asks whether a broadly pretrained model (RoBERTa) still benefits from a second phase of masked-word pretraining on text closer to the target task. The study covers 4 domains (biomedical papers, CS papers, news, reviews) and 8 classification tasks, including low-resource ones with ≤5K labels.
- **DAPT (domain-adaptive pretraining):** continue pretraining on a large domain corpus (2–8B tokens per domain, 12.5K steps). It improved every domain. Gains were largest for domains least similar to RoBERTa’s original training text (biomedical, CS), e.g. ACL-ARC rose from 63.0 to 75.4 F1.
- Pretraining on an _irrelevant_ domain usually hurt, scoring below plain RoBERTa. More data only helps when it’s relevant.
- **TAPT (task-adaptive pretraining):** continue pretraining on just the task’s own unlabeled training text, for 100 epochs with a new random 15% of words masked each epoch.
    - It beat RoBERTa on all 8 tasks and matched or beat DAPT on 5 of them, despite a far smaller corpus.
- **DAPT followed by TAPT was best on every task**: learn the domain first, then the specific task. The authors speculate the reverse order would make the model forget what TAPT taught it.
- **TAPT is task-specific:** a model adapted to one task’s text did _worse_ when fine-tuned on a different task in the same domain (up to 7.7 F1 lower).
- **Curated-TAPT:** pretraining on extra unlabeled text from the same distribution as the task gave further gains.
    - With only 500 labels (0.3% of the RCT dataset), it reached 95% of the performance of DAPT + TAPT trained on the full labeled set.
- **kNN-TAPT** (k-nearest-neighbor selection) is the fallback when you have no extra task text. Embed the task sentences, retrieve similar sentences from a large domain corpus, and add them to the TAPT corpus. It beat plain TAPT everywhere and approached DAPT as more neighbors were retrieved.

#### Don't Stop Pretraining? Make Prompt-based Fine-tuning Powerful Learner (PCP)
- Revisits TAPT across 16 tasks (8 single-sentence, 8 sentence-pair) using RoBERTa-large, in both semi-supervised (16 labels per class) and fully supervised settings. Conventional TAPT turns out to be **not consistently helpful**.
- **Background on fine-tuning styles:**
    - **CLS-based fine-tuning** adds a new classification layer on top of the model’s summary token.
    - **Prompt-based fine-tuning** rewrites the input as a fill-in-the-blank, e.g. “\<text> It was \[MASK].”, and has the model predict a _label word_ such as “great” or “terrible”.
    - A **verbalizer** maps each class to its label word.
    - **Hard prompts** use hand-written templates. **Soft prompts** use learned token embeddings instead of real words.
- **Where TAPT fails:**
    - It hurt CLS-based fine-tuning on 6 of 8 sentence-pair tasks.
    - With prompt-based fine-tuning in the semi-supervised setting, it hurt 12 of 16 tasks, with an average 9.5-point drop on sentence-pair tasks.
    - Single-sentence tasks with CLS-based fine-tuning still mostly benefited (7 of 8).
- **PCP (prompt-based continued pretraining) method:**
	- ![[pcp.png]]
    1. **Train a Draft Model:** Fine-tune a foundation model on your small batch of labeled data so it learns to predict the `[MASK]`token (e.g., `great` or `terrible`).
	    - Traditional FT: ![[traditional_ft.png|515]]
	    - Prompt-based FT: ![[Pasted image 20261012114845.png|518]]
    2. **Generate Pseudo-Labels:** Run your large batch of unlabeled data through the draft model to guess their labels.
    3. **Build the PCP Corpus:** Instead of keeping the text raw, combine the text, prompt template, and labels into complete sentences (e.g., _"I fell asleep. The movie was terrible."_).
    4. **Run Continued Pre-Training (The Core Step):** Take a fresh foundation model and run standard unsupervised Masked Language Modeling (randomly hiding 15% of words) on the formatted corpus from Step 3.
    5. **Final Fine-Tuning:** Take the model from Step 4 and do a final supervised fine-tuning pass using only your perfect, golden labeled data.

- No architecture changes and the same cost as TAPT. The only difference is the extra template and label tokens in the pretraining text.
- **Results:** PCP improved prompt-based fine-tuning by an average of 6.8 points in the semi-supervised setting and about 1 point in the fully supervised setting. Its best case was QNLI, +20.1 points, where TAPT caused a 9.2-point drop.
- **Versus semi-supervised learning:** on 5 standard text benchmarks, PCP beat FixMatch, Dash, FlexMatch and AdaMatch on 4 of 5. It averaged about 2 points better while skipping iterative pseudo-labeling and data augmentation.
- **Robustness:**
    - PCP with _random_ labels still beat no-PCP in 19 of 32 cases, but accurate pseudo-labels clearly matter most.
    - The ablation needs both pieces: templates alone or labels alone lost most of the gain.
    - Simply fine-tuning 5× longer after TAPT added only 0.1 points.


### PEFT
- Subset:
	- ![[Pasted image 20261019132025.png|300]]
- Adapters:
	- ![[Pasted image 20261019132136.png]]
- LoRA:
	- ![[Pasted image 20261019132233.png]]

#### Parameter-Efficient Transfer Learning for NLP (Adapters)
- **Goal:** solve a stream of tasks with one shared model. Freeze BERT and train only a small new module per task, instead of storing a fully fine-tuned copy for each task.
- **Architecture:**
    - Two **bottleneck adapters** go in each transformer layer: one after the attention block, one after the feed-forward block.
    - Each adapter shrinks the representation, applies a nonlinearity, then expands it back, with a skip connection around it.
    - Per task, only the adapters, the layer-norm parameters and the final classifier are trained.
- **Near-identity initialization:** adapter weights start close to zero, so with the skip connection each adapter initially passes its input through unchanged. Training was stable when initial weights were small (std ≤ 0.01) and degraded when they were too large.
- **GLUE (BERT-large):** adapters scored 80.0 vs. 80.4 for full fine-tuning, training 3.6% of parameters per task. Covering all 9 tasks needed 1.3× BERT’s size in total, versus 9× for full fine-tuning.
- **17 extra classification tasks (BERT-base):** 0.4 points behind full fine-tuning, using 1.14% new parameters per task. That’s 1.19× total versus 17× for full fine-tuning.
- **SQuAD question answering:** adapters using 2% of parameters reached 90.4 F1 vs. 90.7 for full fine-tuning. Even tiny adapters (0.1% of parameters) reached 89.9.
- **Versus fine-tuning only the top layers:** on MNLI, a size-64 adapter (~2M params) got 83.7%, while fine-tuning just the top layer (~9M params) got 77.8%. Training only the layer-norm parameters lost 3.5–4 points.
- **Ablation:**
    - Removing any single layer’s adapters cost at most 2 points.
    - Removing all of them dropped the model to majority-class guessing.
    - Lower-layer adapters mattered least, so adapters naturally focus on the top layers.
- **Robust to size:** adapter sizes 8, 64 and 256 averaged 86.2%, 85.8% and 85.7%, so one fixed size works for most tasks. Fancier variants (deeper adapters, parallel placement, added normalization) didn’t beat the simple design.
- Code: google-research/adapter-bert.

#### LoRA: Low-Rank Adaptation of Large Language Models
- **Core idea:** the _change_ in weights needed to adapt a model has a low “intrinsic rank”, meaning it can be described by a few directions. So freeze each weight matrix and learn its update as the product of two thin matrices, B and A.
- **Setup details:**
    - B = 0, so the update is zero at the beginning of training.
    - The update is scaled by α/r (α is a constant, r is the rank). This makes switching r less likely to require re-tuning the learning rate.
    - Most experiments adapt only the attention query and value matrices.
- **No inference latency:** after training, the update is added into the frozen weights. Swapping tasks means subtracting one update and adding another.
    - By contrast, adapters slowed GPT-2 medium inference by 20–30% at batch size 1.
- **GPT-3 175B savings:**
    - Training memory: 1.2TB → 350GB.
    - Checkpoint size: 350GB → 35MB (~10,000× smaller).
    - Training: about 25% faster.
    - Storing 100 task versions: ~354GB instead of ~35TB.
- **Quality:**
    - Matched or beat full fine-tuning on GPT-3, e.g. 4.7M params gave 73.4 on WikiSQL vs. 73.8 for full fine-tuning, and 91.7 vs. 89.5 on MNLI.
    - On GLUE: RoBERTa-base 87.2 vs. 86.4 for full fine-tuning; DeBERTa-XXL 91.3 vs. 91.1.
- **Which matrices to adapt:** with a fixed parameter budget, adapting more matrices at low rank beats one matrix at higher rank. Query + value at rank 4 beat query alone at rank 8.
- **How small r can be:** rank 1 was already enough for query + value on GPT-3. Different ranks and random seeds learned mostly the same top direction, **suggesting extra rank mostly adds noise**.
- **What the update does:** it amplifies directions already present in the weights but not emphasized by pretraining, by roughly 20× at rank 4. In effect **it boosts task-relevant features the model already has**.
- **Low data:** on MNLI with only 100 examples, LoRA scored 63.8 vs. 60.2 for full fine-tuning. Prefix-tuning nearly collapsed to chance level.
- **Limitations:**
    - Once merged, it’s hard to batch inputs for different tasks in a single pass.
    - Small r may not suffice for very different tasks, e.g. a new language.
    - Choosing which matrices to adapt is still heuristic.

#### QLoRA: Efficient Finetuning of Quantized LLMs
- **Core idea:** store the frozen base model in 4-bit, keep LoRA adapters in 16-bit, and pass gradients through the 4-bit model into the adapters. During each forward and backward pass, weights are temporarily converted back to 16-bit for the computation.
- **Memory:** fine-tuning LLaMA-65B normally needs over 780GB of GPU memory. QLoRA brings it under 48GB, a single GPU, without losing quality versus 16-bit.
- **Three new pieces:**
    - **4-bit NormalFloat (NF4):** a 4-bit format whose 16 values are spaced to match the bell-curve shape of trained weights, so each value bucket gets used about equally.
    - **Double quantization:** also compress the scaling constants used by quantization. This saves ~0.37 bits per parameter, about 3GB on a 65B model.
    - **Paged optimizers:** automatically move optimizer memory to CPU RAM when the GPU briefly runs out, preventing crashes during long sequences.
- **Critical LoRA setting:** LoRA on only query and value (the original default) did _not_ match 16-bit quality. Adapters had to go on **all linear layers**. Once they did, the rank r barely mattered.
- **Matches 16-bit:**
    - GLUE with RoBERTa-large: 88.6 for full 16-bit fine-tuning, 88.8 for 16-bit LoRA; QLoRA variants scored 88.6–88.8.
    - MMLU (a 57-subject knowledge test) on LLaMA 7–65B: NF4 averaged 53.1 vs. 53.0 for 16-bit. FP4 was ~1 point behind.
- **Guanaco chatbots:**
    - 65B reached 99.3% of ChatGPT’s score on the Vicuna benchmark after 24 hours on one GPU.
    - 33B was trainable on a 24GB consumer GPU in under 12 hours.
    - 7B fits in ~5GB.
- **Data quality beats size:** a 9K-example curated dataset (OASST1) beat a 450K subsample of FLAN v2 for chatbot quality. More data or epochs added at most 0.5 MMLU points, while switching datasets changed scores by up to 8.
- **Benchmarks measure different things:** FLAN v2 was best on MMLU but worst as a chatbot. Strong scores on one don’t predict the other.
- **Evaluation caveats:** GPT-4 as a judge roughly agrees with humans on system rankings, but agreement on individual examples is weak. GPT-4 also favors whichever answer is shown first and rates its own outputs higher.
- **Limitations:** matching full 16-bit fine-tuning wasn’t verified at 33B/65B, other PEFT methods and bit-widths weren’t tested, and the bias and safety evaluation was limited.
- Code: artidoro/qlora; bitsandbytes (integrated into Hugging Face).
