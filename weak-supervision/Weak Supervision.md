## Reading
### Introduction
- [x] [Weak Supervision: A New Programming Paradigm for Machine Learning](https://ai.stanford.edu/blog/weak-supervision/)
- [ ] [A brief introduction to weakly supervised learning](https://academic.oup.com/nsr/article/5/1/44/4093912) (This may be using "weakly supervised learning in a different context)
### Papers
- [x] [Weak Supervision Survey (2022)](https://arxiv.org/abs/2202.05433)
- [ ] [Weak Supervision Survey (2025)](https://wires.onlinelibrary.wiley.com/doi/10.1002/widm.70022) (Tied to the paper *A brief introduction to weakly supervised learning*)
- [x] [Awesome Weak Supervision GitHub](https://github.com/michael-aloys/awesome-weak-supervision)

## Benchmark(s)
- [WRENCH: A Comprehensive Benchmark for Weak Supervision](https://arxiv.org/abs/2109.11377)

## Advancements
- Snorkel: main weak supervision framework
- Skweak: weak supervision for NER extraction
- [Language Models in the Loop: Incorporating Prompting into Weak Supervision](https://arxiv.org/abs/2205.02318)
- [Alfred](https://arxiv.org/abs/2305.18623)

## Tutorials
- [x] [Snorkel Intro Tutorial: Data Labeling](https://snorkelproject.org/use-cases/01-spam-tutorial/)
- [ ] [Argilla Weak Supervision](https://docs.v1.argilla.io/en/v1.1.0/guides/techniques/weak_supervision.html)
	- Higher-level abstraction of Snorkel
- [ ] [NER Weak Supervision](https://github.com/NorskRegnesentral/skweak)

## Tools
- [Snorkel](https://github.com/snorkel-team/snorkel)
- [Cleanlab](https://github.com/cleanlab/cleanlab)
- [Knodle](https://github.com/knodle/knodle)
	- [ ] [Paper](https://arxiv.org/abs/2104.11557)
- [ANEA](https://github.com/uds-lsv/anea)
- [Skweak](https://github.com/NorskRegnesentral/skweak)
	- [ ] [Paper](https://aclanthology.org/2021.acl-demo.40/)

## Notes
### Weak Supervision: A New Programming Paradigm for Machine Learning
- Problem(s): 
	- State-of-the-art models require mass amounts of unlabeled data
	- Labeling guidelines, granularities, or downstream use cases change which results in the need to re-label
- Weak supervision definition: training a model using data that has been generated through external knowledge bases, patterns/rules, or other classifiers
	- Data used to train these models are often called programming training data
	- many noisy votes → one smart aggregation step → one soft label per example → train end model on that
- Snorkel approach:
	1. Users write labeling functions AKA LFs (code functions acting as decision rules) that label subsets of unlabeled data
		- LFs can be task-specific heuristics, regex pattern matching, rules-of-thumb, negative label generation, etc.
	2. A generative model is used to learn the accuracies of the labeling functions and to weight the outputs (probabilistic labels: 0.90, 0.65, 0.55, 0.80, etc.)
		- Goal of the generative model is to estimate $P(L|y)$
			- $L$ = output of labels by the LFs
			- $y$ = the true label (unkown)
	3. A DNN trained on the original unlabeled data with the probabilistic labels as the target outputs

**Example:**

| Input $x$ (raw text)                                              | Target $y$ (probabilistic label) |
| ----------------------------------------------------------------- | -------------------------------- |
| "Congratulations! You've won a FREE prize!!! Click now to claim." | 0.93                             |
| "Hey, here's that free ebook I mentioned, no strings attached."   | 0.80                             |
| "Hi Mom, dinner on Sunday? Let me know what time works."          | 0.04                             |
| "FREE trial ending soon!!! Renew now or lose access."             | 0.55                             |
| "Can't believe the game last night!!! Insane finish."             | 0.65                             |

### 2022 Survey
- Label function forms:
	- User-written heuristics
	- Existing knowledge bases
	- Pre-trained models
	- Third-party tools
	- Crowd-sourced labeling
- How to generate LFs:
	- Automatic generation: 
		- [Snuba: Automating Weak Supervision to Label Training Data](https://pmc.ncbi.nlm.nih.gov/articles/PMC6879381/)
		- [Weakly Supervised Named Entity Tagging with Learnable Logical Rules](https://aclanthology.org/2021.acl-long.352.pdf)
		- [GLaRA: Graph-based Labeling Rule Augmentation for Weakly Supervised Named Entity Recognition](https://aclanthology.org/2021.eacl-main.318.pdf)
	- Interactive generation:
		- [DARWIN: Adaptive Rule Discovery for Labeling Text Data](https://dl.acm.org/doi/epdf/10.1145/3448016.3457334)
		- [Interactive Weak Supervision: Learning Useful Heuristics for Data Labeling](https://arxiv.org/abs/2012.06046)
	- Guided Generation
		- [Interactive Programmatic Labeling for Weak Supervision](https://bencw99.github.io/files/kdd2019_dcclworkshop.pdf)


### A brief introduction to weakly supervised learning
- Refers to "Weak" supervision as anything that is not "strong" supervision. This is different than what snorkel or has developed in the way of LFs and LabelModels
- 3 different types of to weakly supervised learning: Incomplete, inexact, and inaccurate
- Incomplete:
	- Only a subset of the data has labels
	- **Active Learning:** SME labels most valuable data
		1. Initial Training: A model is trained on a very small set of manually labeled data.
		2. Prediction & Evaluation: The model runs predictions on a massive pool of unlabeled data and measures its own confidence or uncertainty.
		3. Querying: The model flags the data points it is most confused about or that would provide the most new information.
		4. Human Annotation: A human expert labels those specific flagged samples.
		5. Retraining: The newly labeled data is added to the training set, the model is retrained, and the cycle repeats.
	- **Semi-supervised Learning:** Uses unlabeled data without a human in the loop
		1. Train the Base Model: Train an initial supervised machine learning model using only the small portion of manually labeled data.
		2. Predict Pseudo-Labels: Run the trained model on the large pool of unlabeled data to generate predicted labels (called **pseudo-labels**) along with probability scores. 
		3. Filter by Confidence: Evaluate the predictions and select only the high-confidence pseudo-labels*(ex: predictions with > 90% probability). Discard or ignore the uncertain ones for this round. 
		4. Expand the Dataset: Concatenate the newly selected pseudo-labeled data with the original, human-labeled training set.
		5. Retrain and Iterate: Re-train the model from scratch on the newly expanded dataset. Repeat steps 2 through 5 until the model stabilizes or no new high-confidence labels are generated.
		- 4 main methods:
			- Generative methods: Assume labeled and unlabeled data come from the same underlying generative model, treating unlabeled labels as missing parameters estimated via approaches like EM.
			- Graph-based methods: Build a graph where nodes are instances and edges reflect similarity, then propagate label information across the graph.
			- Low-density separation methods: Push the classification boundary through low-density regions of the input space, as exemplified by S3VMs (semi-supervised SVMs).
			- Disagreement-based methods: Train multiple learners that teach each other by treating their confidently-predicted unlabeled instances as pseudo-labels, with co-training (using two different feature views) as the most well-known example.
- Inexact:
	- Labels exist but are coarse-grained. For example there exists 1 label for an image that contains many subjects or a single label for a box containing many items.
- Inaccurate
	- Labels exist but they are not always true
	1. Noisy labels
	2. Crowdsourcing: labels come from many independent workers of unknown and varying reliability

### Snuba: Automating Weak Supervision to Label Training Data
- Synthesizer: create candidate heuristics
	- - **Takes in:** the labeled data. On the first round that's the full labeled set; on later rounds it's only the labeled points the verifier flagged as still uncertain.
	- **Produces:** a pool of candidate heuristics, each of which labels a point positive or negative, or abstains.
	- Encourages highly accurate data over high coverage data
- Pruner: take the single best heuristic
	- It scores each candidate on two things: how well it performs on the labeled data, and how much it labels unlabeled points that no existing heuristic has covered yet. Adds the best balance of the 2 metrics.
		- Jaccard distance: "How unique is this rule compared to the ones we already have"
		- Paired together with the synthesizer to balance the highest accuracy with the highest diversity
	- **Takes in:** the candidate pool from the synthesizer, the current committed set of heuristics, the labeled data, and the unlabeled data.
	- **Produces:** one chosen heuristic, which is added to the committed set.
- Verifier: combine labels, check quality, and decide what's next
	- It runs a label aggregator (a generative model) that estimates how trustworthy each heuristic is without seeing true labels, then combines their votes into a confidence-weighted label for each point.
		- It compares the aggregator's estimate of each heuristic's accuracy against that heuristic's actual accuracy on the small labeled set. If they disagree too much, a recently added heuristic is probably worse than random on the unlabeled data. In that case Snuba stops and keeps the labels from the previous round.
		- Otherwise, it finds the labeled points that still have low-confidence labels and sends them back to the synthesizer. The next heuristic can then focus on those hard cases. If no such points remain, the loop also ends.
	- Without a verifier, an automated method can continue to generate heuristics that deteriorate the overall quality of the end model
	- **Takes in:** the committed set of heuristics, the labeled data, and the unlabeled data.
	- **Produces:** probabilistic training labels for the unlabeled data, plus either a subset of low-confidence labeled points for the next round or a signal to stop.