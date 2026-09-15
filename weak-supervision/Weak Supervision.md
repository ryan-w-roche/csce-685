## Reading
### Introduction
- [x] [Weak Supervision: A New Programming Paradigm for Machine Learning](https://ai.stanford.edu/blog/weak-supervision/)
- [ ] [A brief introduction to weakly supervised learning](https://academic.oup.com/nsr/article/5/1/44/4093912) (This may be using "weakly supervised learning in a different context)
### Papers
- [x] [Weak Supervision Survey (2022)](https://arxiv.org/abs/2202.05433)
- [ ] [Weak Supervision Survey (2025)](https://wires.onlinelibrary.wiley.com/doi/10.1002/widm.70022) (Tied to the paper *A brief introduction to weakly supervised learning*)
- [x] [Awesome Weak Supervision GitHub](https://github.com/michael-aloys/awesome-weak-supervision)
- [ ] [Stanford CS229](https://cs229.stanford.edu/notes2019fall/weak_supervision_notes.pdf)
## Tutorials
- [x] [Snorkel Intro Tutorial: Data Labeling](https://snorkelproject.org/use-cases/01-spam-tutorial/)
- [ ] [Argilla Weak Supervision](https://docs.v1.argilla.io/en/v1.1.0/guides/techniques/weak_supervision.html)
- [ ] [NER Weak Supervision](https://github.com/NorskRegnesentral/skweak)
## Tools
- [Snorkel](https://github.com/snorkel-team/snorkel)
- [Cleanlab](https://github.com/cleanlab/cleanlab)
- [Knodle](https://github.com/knodle/knodle)
	- [ ] [Paper](https://arxiv.org/abs/2104.11557)
- [ANEA](https://github.com/uds-lsv/anea)
- [Skweak](https://github.com/NorskRegnesentral/skweak)

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


