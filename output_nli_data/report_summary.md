# Experiment 1a Canonical Run

Date: 2026-09-08. Status: all six configured models completed; all predictions and PCA plots validated.

Canonical location: [`experiment1/outputs/experiment1a/20260908-approved-roles/`](experiment1/outputs/experiment1a/20260908-approved-roles/).
Existing old results, plots, snapshots and other outputs were not overwritten. They are now retained under [archive/experiment1/](archive/experiment1/); see the [relocation map](archive/README.md).
Only [experiment1/data/experiment1_rows.csv](experiment1/data/experiment1_rows.csv) was regenerated for this run, not [experiment1/data/experiment1b_rows.csv](experiment1/data/experiment1b_rows.csv).

## Task

- Model premise: CSV `premises` + one space + CSV `target_sentence` (outer whitespace stripped).
- Model conclusion: CSV `conclusion`, a fully verbalized German once/twice/cannot-say answer, not the target sentence alone.
- Once uses `hat einmal ...`; twice uses `hat mindestens zweimal ...`; cannot say uses `Es lässt sich nicht sagen, wie oft ... hat.`
- Results retain every generated input field and record the exact strings as `model_premise` and `model_conclusion`.
- 40 items x 2 contexts x 2 targets x 2 brace choices x 3 responses = **960 unique rows per model**, **5,760 predictions total**.
- Each condition has 480 rows; each response option has 320 rows. Gold remains 320 `entailment` and 640 `unknown` rows per model.

## Models And Artifacts

These are the actual six checkpoints used, with no substitutions. Match counts are descriptive agreement with the retained behavioral mapping, **not strict logical NLI accuracy**.

| Model | Rows | Behavioral Matches | Results CSV | PCA Plot |
|-------|------|--------------------|-------------|----------|
| `mtc/gbert-large-xnli-de-finetuned` | 960 | 644 (67.08%) | [CSV](experiment1/outputs/experiment1a/20260908-approved-roles/predictions/mtc_gbert-large-xnli-de-finetuned.csv) | [PNG](experiment1/outputs/experiment1a/20260908-approved-roles/plots/mtc_gbert-large-xnli-de-finetuned_pca2d.png) |
| `Sahajtomar/German_Zeroshot` | 960 | 640 (66.67%) | [CSV](experiment1/outputs/experiment1a/20260908-approved-roles/predictions/Sahajtomar_German_Zeroshot.csv) | [PNG](experiment1/outputs/experiment1a/20260908-approved-roles/plots/Sahajtomar_German_Zeroshot_pca2d.png) |
| `morit/german_xlm_xnli` | 960 | 636 (66.25%) | [CSV](experiment1/outputs/experiment1a/20260908-approved-roles/predictions/morit_german_xlm_xnli.csv) | [PNG](experiment1/outputs/experiment1a/20260908-approved-roles/plots/morit_german_xlm_xnli_pca2d.png) |
| `joeddav/xlm-roberta-large-xnli` | 960 | 436 (45.42%) | [CSV](experiment1/outputs/experiment1a/20260908-approved-roles/predictions/joeddav_xlm-roberta-large-xnli.csv) | [PNG](experiment1/outputs/experiment1a/20260908-approved-roles/plots/joeddav_xlm-roberta-large-xnli_pca2d.png) |
| `FacebookAI/roberta-large-mnli` | 960 | 638 (66.46%) | [CSV](experiment1/outputs/experiment1a/20260908-approved-roles/predictions/FacebookAI_roberta-large-mnli.csv) | [PNG](experiment1/outputs/experiment1a/20260908-approved-roles/plots/FacebookAI_roberta-large-mnli_pca2d.png) |
| `jabo/bert-base-german-cased-xnli-de` | 960 | 317 (33.02%) | [CSV](experiment1/outputs/experiment1a/20260908-approved-roles/predictions/jabo_bert-base-german-cased-xnli-de.csv) | [PNG](experiment1/outputs/experiment1a/20260908-approved-roles/plots/jabo_bert-base-german-cased-xnli-de_pca2d.png) |

The existing visualization script projects the three NLI probabilities into two PCA dimensions, with separate response panels, condition colors and label anchors. PCA is fitted separately for each model, so axes are not a shared cross-model coordinate system.

### Academic Origins

Sources checked: **2026-09-08**. The table distinguishes evidence about the **exact tested checkpoint** from papers about its architecture, base checkpoint, training corpus or methodology. HF cards/configs are repository documentation, not peer-reviewed papers; a card citing a paper is not evidence that the paper mentions that downstream checkpoint. No direct academic mention of these six exact HF identifiers was identified in the consulted primary sources. This is a bounded provenance check of the linked sources below, not an exhaustive citation search or a claim that such mentions cannot exist. General web searches did not yield usable additional evidence.

| Exact Tested Checkpoint And Primary Evidence | Architecture And Fine-Tuning Evidence | Academic Relationship And Limits |
|---|---|---|
| `mtc/gbert-large-xnli-de-finetuned`: [HF page](https://huggingface.co/mtc/gbert-large-xnli-de-finetuned), [config](https://huggingface.co/mtc/gbert-large-xnli-de-finetuned/resolve/main/config.json). No model card; raw `README.md` returned 404. | Config declares `BertForSequenceClassification`, 24 layers, hidden size 1024, and `finetuning_task: xnli`. Its saved local `_name_or_path` contains `deepset-gbert-large` and `gbert_large_xnli_de_finetuning_all_labels`, supporting a GBERT-large/German-XNLI lineage, but not documenting the actual data splits or training recipe. | **Indirect:** GBERT [G], BERT [B], and XNLI/MultiNLI [X, M] are the relevant base/architecture and indicated corpus foundations. The [GBERT-large card](https://huggingface.co/deepset/gbert-large/raw/main/README.md) links [G]; that paper does not establish this later `mtc` fine-tune. **No checkpoint-specific paper identified in consulted sources.** No academic affiliation inferred from the uploader name or saved path. |
| `Sahajtomar/German_Zeroshot`: [HF card](https://huggingface.co/Sahajtomar/German_Zeroshot/raw/main/README.md), [config](https://huggingface.co/Sahajtomar/German_Zeroshot/resolve/main/config.json). | Card explicitly names `deepset/gbert-large` fine-tuned on German XNLI; config confirms the base name and 24-layer BERT classifier. Despite the card's `multilingual` metadata, its description calls it **monolingual** and recommends German hypotheses. Split construction and detailed optimization settings are not supplied. | **Indirect:** [G] is the base checkpoint's paper, [B] the architecture/fine-tuning foundation, and [X, M] the NLI corpus lineage. GBERT's deepset-associated authorship is documented in its base card, not evidence that those authors produced or endorsed this upload. **No checkpoint-specific paper identified in consulted sources.** |
| `morit/german_xlm_xnli`: [HF card](https://huggingface.co/morit/german_xlm_xnli/raw/main/README.md), [config](https://huggingface.co/morit/german_xlm_xnli/resolve/main/config.json). | Config explicitly names **`cardiffnlp/twitter-xlm-roberta-base`**, with a 12-layer `XLMRobertaForSequenceClassification` architecture. The [parent card](https://huggingface.co/cardiffnlp/twitter-xlm-roberta-base/raw/main/README.md) and [T, section 2.1](https://arxiv.org/html/2104.12250v2#S2.SS1) verify XLM-R-base continued MLM pretraining on about 198M multilingual tweets. The `morit` card then documents German machine-translated MNLI/XNLI training for five epochs, selecting by validation accuracy (learning rate `2e-5`, batch 32, maximum length 128). | **Indirect, verified chain:** XLM-R [R] -> Twitter-adapted XLM-T [T] -> this German NLI fine-tune [X, M]. XLM-T is relevant here, not a mistaken attribution based on a similar name, but it is **the parent's paper, not a paper introducing `morit/german_xlm_xnli`**. [T] lists Snap Inc. and Cardiff University affiliations for its own authors; these are not established affiliations of `morit`. Its sentiment/adaptor experiments do not establish this checkpoint's NLI training recipe. **No checkpoint-specific paper identified in consulted sources.** |
| `joeddav/xlm-roberta-large-xnli`: [HF card](https://huggingface.co/joeddav/xlm-roberta-large-xnli/raw/main/README.md), [config](https://huggingface.co/joeddav/xlm-roberta-large-xnli/resolve/main/config.json). | XLM-R-large, confirmed as a 24-layer XLM-R classifier. The card documents NLI fine-tuning on concatenated **MNLI training plus XNLI validation and test sets**, followed by one additional XNLI epoch with premise/hypothesis translations shuffled across languages for the same original example. This is not merely German-XNLI training. | **Indirect:** XLM-R [R] is the base model paper; [X, M] describe the NLI resources. The multilingual fine-tuning recipe is documented by the uploader, not attributed to [R]. Its inclusion of XNLI validation/test data means those splits cannot be treated as held-out evaluation for this checkpoint. **No checkpoint-specific paper identified in consulted sources.** |
| `FacebookAI/roberta-large-mnli`: [HF card](https://huggingface.co/FacebookAI/roberta-large-mnli/raw/main/README.md), [config](https://huggingface.co/FacebookAI/roberta-large-mnli/resolve/main/config.json). | English RoBERTa-large fine-tuned on MNLI, with a 24-layer `RobertaForSequenceClassification` architecture. The card documents English MLM pretraining on BookCorpus, Wikipedia, CC-News, OpenWebText and Stories. The card-linked [official fairseq release](https://github.com/facebookresearch/fairseq/blob/main/examples/roberta/README.md) explicitly lists `roberta.large.mnli`. | **Original-research/release connection:** the card designates Liu et al. [O] as its research paper and citation; [O, section 5.1](https://arxiv.org/html/1907.11692v1#S5.SS1) describes MNLI fine-tuning, and its associated implementation releases the named MNLI variant. This is stronger than a community derivative's architecture-only citation, but **not a verified mention of the exact `FacebookAI/...` HF identifier or proof of byte-identical paper/run weights**. No separate HF-checkpoint-specific paper identified in consulted sources. [M] is the corpus paper. Facebook AI and University of Washington affiliations are given in [O]. |
| `jabo/bert-base-german-cased-xnli-de`: [HF page](https://huggingface.co/jabo/bert-base-german-cased-xnli-de), [config](https://huggingface.co/jabo/bert-base-german-cased-xnli-de/resolve/main/config.json). No model card; raw `README.md` returned 404. | Config names `bert-base-german-cased`, a 12-layer BERT sequence classifier with NLI labels. Its [base card](https://huggingface.co/bert-base-german-cased/raw/main/README.md) documents deepset's 2019 German BERT release, pretrained on German Wikipedia, OpenLegalData and news. German-XNLI fine-tuning is **indicated by the repository name**, not independently specified by a training card; splits and optimization are unknown. | **Indirect:** BERT [B] supplies the architecture/methodology; [X, M] are the indicated corpus lineage. The German base release is documented by its authors' card, not by treating the later GBERT paper [G] as this model's origin. Neither the original Google BERT authors nor deepset are thereby established as authors of the `jabo` fine-tune. **No checkpoint-specific paper identified in consulted sources.** |

**Shared academic references.** These explain lineage, not endorsement of the tested checkpoints, their suitability for Tiemann's items, or the behavioral scores above. XNLI [X] extends MultiNLI development/test material to 15 languages; the German training material commonly called "XNLI train" is machine-translated MultiNLI, distinct from those translated evaluation sets. Missing downstream training documentation cannot be filled in from a base-model paper. The checked HF `main` sources are mutable and do not retrospectively pin the canonical run's model revisions.

- **[G] GBERT:** Branden Chan, Stefan Schweter and Timo Möller (2020). *German's Next Language Model*. COLING. [ACL/paper](https://aclanthology.org/2020.coling-main.598/); [DOI: 10.18653/v1/2020.coling-main.598](https://doi.org/10.18653/v1/2020.coling-main.598). Introduces GBERT/GELECTRA, not the later NLI uploads.
- **[B] BERT:** Jacob Devlin, Ming-Wei Chang, Kenton Lee and Kristina Toutanova (2019; preprint 2018). *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*. NAACL-HLT. [ACL/paper](https://aclanthology.org/N19-1423/); [DOI: 10.18653/v1/N19-1423](https://doi.org/10.18653/v1/N19-1423). Architecture, pretraining and task-specific fine-tuning foundation.
- **[R] XLM-R:** Alexis Conneau, Kartikay Khandelwal, Naman Goyal, Vishrav Chaudhary, Guillaume Wenzek, Francisco Guzmán, Edouard Grave, Myle Ott, Luke Zettlemoyer and Veselin Stoyanov (2020; preprint 2019). *Unsupervised Cross-lingual Representation Learning at Scale*. ACL. [ACL/paper](https://aclanthology.org/2020.acl-main.747/); [DOI: 10.18653/v1/2020.acl-main.747](https://doi.org/10.18653/v1/2020.acl-main.747). Introduces XLM-R, pretrained on filtered CommonCrawl in 100 languages.
- **[T] XLM-T:** Francesco Barbieri, Luis Espinosa Anke and Jose Camacho-Collados (2022; preprint 2021). *XLM-T: Multilingual Language Models in Twitter for Sentiment Analysis and Beyond*. LREC. [ACL/paper](https://aclanthology.org/2022.lrec-1.27/); [arXiv:2104.12250](https://arxiv.org/abs/2104.12250); [arXiv DOI: 10.48550/arXiv.2104.12250](https://doi.org/10.48550/arXiv.2104.12250). The ACL record lists no proceedings DOI; the DOI here identifies the preprint. Documents the Twitter-adapted parent, not the German XNLI derivative.
- **[O] RoBERTa:** Yinhan Liu, Myle Ott, Naman Goyal, Jingfei Du, Mandar Joshi, Danqi Chen, Omer Levy, Mike Lewis, Luke Zettlemoyer and Veselin Stoyanov (2019). *RoBERTa: A Robustly Optimized BERT Pretraining Approach*. [arXiv:1907.11692/full paper](https://arxiv.org/html/1907.11692v1); [DOI: 10.48550/arXiv.1907.11692](https://doi.org/10.48550/arXiv.1907.11692). Pretraining recipe and downstream MNLI experiments; the official HF card's requested citation.
- **[X] XNLI:** Alexis Conneau, Ruty Rinott, Guillaume Lample, Adina Williams, Samuel R. Bowman, Holger Schwenk and Veselin Stoyanov (2018). *XNLI: Evaluating Cross-lingual Sentence Representations*. EMNLP. [ACL/paper](https://aclanthology.org/D18-1269/); [DOI: 10.18653/v1/D18-1269](https://doi.org/10.18653/v1/D18-1269). Cross-lingual NLI resource and transfer methodology, not a paper for these later checkpoints.
- **[M] MultiNLI/MNLI:** Adina Williams, Nikita Nangia and Samuel R. Bowman (2018; preprint 2017). *A Broad-Coverage Challenge Corpus for Sentence Understanding through Inference*. NAACL-HLT. [ACL/paper](https://aclanthology.org/N18-1101/); [DOI: 10.18653/v1/N18-1101](https://doi.org/10.18653/v1/N18-1101). English NLI corpus underlying MNLI fine-tuning and XNLI's corpus lineage.

## Corrections And Provenance

- [experiment1/generate_experiment1_csv.py](experiment1/generate_experiment1_csv.py) now uses explicit `ROLE_EXCEPTIONS` metadata: items 3/4 have agent-first braces in `ai`; items 32/39 have agent-oriented `bi` and recipient-oriented `bii`. All eight condition cells per exception invert, affecting 96 row conditions and their condition-bearing IDs. The gold scheme itself is unchanged; 64 gold labels change because once/twice swap, while cannot-say remains `unknown`.
- Source text and brace order for these items were preserved. `role_note` explains exceptions in generated rows and results.
- Item 20 `bii` was changed in [experiment1/extract_experiment1_items.py](experiment1/extract_experiment1_items.py) `CURATED_OVERRIDES`, never by hand-editing [JSON](experiment1/data/experiment1_items.json). The exact user-approved editorial reconstruction is:

> Vor zwei Wochen hat {Karl/Greta} wieder einem Freund ein französisches Lied beigebracht, als {er/sie} mit einem Freund unterwegs war.

- The extractor preserves the printed duplicate under `bii_source_text`, retains `bii_inferred` and updates `bii_note` to identify user approval and replacement of the earlier *gesungen* reconstruction. The PDF is the source of truth; this single override is explicitly not verbatim PDF text.
- Only the 12 affected item-20 `bii` rows carry `target_inferred=True` and the reconstruction `target_note`. Both fields propagate unchanged into every results CSV; all other rows have `False` and an empty note.
- The runner already concatenated context and target before this work. It now enforces CSV `conclusion`, removes the alternate `--hypothesis-column` option, uses conclusion terminology, and records actual model inputs.
- [AGENTS.md](AGENTS.md) and [experiment1/experiment1_schema.md](experiment1/experiment1_schema.md) now describe the experiment-1 task, exceptions and provenance. Experiment-2 instructions remain context-as-premise and target-as-conclusion/hypothesis.

## Execution

Commands were run from `/Users/princess_zelda/Desktop/tiemann.nli` using the existing venv. Parent directories were checked with `ls` before creating run artifacts. The inference command was launched with `nohup` in the background to avoid tool timeout interruption and monitored through completion; its output is retained in [run.log](experiment1/outputs/experiment1a/20260908-approved-roles/run.log).

The following is the **historical execution transcript**, not a cleanup rerun recipe.
At execution time, generator/runner defaults used data files directly under `experiment1/`;
those files now live in `experiment1/data/`. The original log remains unchanged, while
the audit's input paths were updated. Use the [README](README.md) for current commands
and new-run output paths; do not rerun this transcript into the preserved canonical directory.

```bash
venv/bin/python experiment1/extract_experiment1_items.py
venv/bin/python experiment1/extract_experiment1_items.py --validate
venv/bin/python experiment1/generate_experiment1_csv.py
venv/bin/python -m unittest discover -s experiment1 -p 'test_*.py'
mkdir -p experiment1/outputs/experiment1a/20260908-approved-roles/predictions experiment1/outputs/experiment1a/20260908-approved-roles/plots
nohup venv/bin/python -u experiment1/run_experiment1_nli.py --output-dir experiment1/outputs/experiment1a/20260908-approved-roles/predictions > experiment1/outputs/experiment1a/20260908-approved-roles/run.log 2>&1 &
venv/bin/python experiment1/visualize_experiment1_nli.py --input experiment1/outputs/experiment1a/20260908-approved-roles/predictions --output-dir experiment1/outputs/experiment1a/20260908-approved-roles/plots
venv/bin/python experiment1/outputs/experiment1a/20260908-approved-roles/validate_run.py
```

For a future refresh, choose a new run ID rather than rerunning the inference/plot commands into this canonical directory.

Environment checks passed: torch 2.11.0, transformers 5.12.1, matplotlib 3.10.9, numpy 2.2.6, sentencepiece importable, and `/opt/homebrew/bin/pdftotext` available. Inference used CPU; MPS was unavailable in this environment. No dependency installation was necessary.

## Validation

- PDF extractor `--validate`: passed, 40 items and 160 fields checked against fresh PDF extraction plus declared curated overrides.
- Minimal regression test: passed, 48 subcases across both contexts, targets and braces for a default item, item 20 and all four exceptions.
- [Run-specific audit](experiment1/outputs/experiment1a/20260908-approved-roles/validate_run.py): passed. It checks all non-overridden fields against PDF extraction, preservation of item 20's printed sentence, exact reconstruction, row counts, unique IDs, role conditions, gold mapping, verbalization markers and provenance.
- All six results have 960 unique IDs and preserve every source-row field in order. Recorded model inputs match the approved task exactly.
- All 5,760 probability vectors are finite and within [0, 1]; maximum absolute score-sum error was approximately `1.38e-7`, below the `1e-6` tolerance. Every predicted label equals score argmax and every `match` field matches the documented gold comparison (`neutral` normalized to `unknown`).
- All six plots exist and pass PNG integrity checks at 3600 x 1200 pixels.
- Scoped `git diff --check` passed. No staging or commits were performed.

## Cautions

The existing gold labels implement Chapter 2's behavioral answer mapping: twice is intended in positive conditions, once in neutral conditions, and other answers receive `unknown`. Unsupported prior events do not logically prove exactly one event; non-intended answers need not be NLI-neutral. These scores must not be presented as strict logical NLI accuracy. The English MNLI RoBERTa checkpoint was deliberately retained among the configured models despite the German inputs.


