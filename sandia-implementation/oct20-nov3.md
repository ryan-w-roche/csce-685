## Architecture

![[685_implementation_v1.png]]

- **Prepare:** MongoDB documents (8,740 rows including revisions) are joined with 455 gold labels across 12 classes and checked against the model’s token limit.
- **Cross-validate:** On the same stratified 3-fold splits, a TF-IDF baseline and a LoRA fine-tuned Gemma-4-31B are scored against the gold labels on macro and rare-class F1.
- **Predict:** The chosen setup is retrained on all 455 labels and classifies the 3,696 unlabeled documents, producing a CSV of labels with confidence scores.

## Next Experiments (Priority Ordered)
- **Field ablation:** retrain TF-IDF on subsets of fields (free text only, structured fields only, without the largest fields) to find which fields carry the signal. May cut tokens per document a lot, and trimming fields isn’t chunking.
- **Repeated CV for error bars:** rerun TF-IDF and the LLM with 3–5 CV repeats. TF-IDF is already strong (macro F1 0.601, rare-class F1 0.499), so you need the spread across repeats to tell whether the LLM’s lead is real.
- **Stronger cheap baseline(s):** tune TF-IDF (C, character n-grams, field-weighted features) and try zero-shot Gemma-4-31B prompting with a written class guide. Few-shot prompting won’t fit: 12 examples × about 16k tokens is more than the context window.
- **Hyperparameter sweep:** a small grid over epochs (2–5), learning rate, LoRA rank (8–32) and class-weight power (0.5 or 1.0), judged on rare-class F1.