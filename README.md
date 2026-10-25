# BERT-Tiny Indic LID

A lightweight multilingual **Indian-language identification (LID)** project built around a fine-tuned BERT-Tiny sequence classifier. This repository is intended to publish the model, its training/evaluation workflow, and reproducible comparisons with existing language-identification systems.

> **Release status:** the repository is being prepared. Checkpoints, tokenizer files, original training notebooks, and distributable dataset files still need to be uploaded and validated before this is a complete reproducible release.

## What is included
- Fine-tuned BERT-Tiny E2/E4 model artifacts (to be uploaded).
- Dataset provenance, split and annotation documentation (to be completed with the exact release dataset).
- Fine-tuning, evaluation, and cross-model comparison notebooks.
- Metrics, confusion matrices, latency measurements, and a benchmark report.
- Inference and deployment guidance.

## Target labels
| Label | Language / meaning |
|---|---|
| `as-IN` | Assamese |
| `bn-IN` | Bengali |
| `en-IN` | English |
| `gu-IN` | Gujarati |
| `hi-IN` | Hindi |
| `kn-IN` | Kannada |
| `ml-IN` | Malayalam |
| `mr-IN` | Marathi |
| `none` | Unsupported, ambiguous, or insufficient evidence according to the dataset's annotation policy |
| `pa-IN` | Punjabi |
| `ta-IN` | Tamil |
| `te-IN` | Telugu |

Read the dataset/model cards for the precise label policy. Do not assume every baseline natively supports every target label.

## Repository structure
- `model/` — model checkpoints and tokenizer release instructions.
- `dataset/` — dataset provenance, licensing, schema, and split documentation.
- `notebooks/` — fine-tuning, model evaluation, and cross-model comparison.
- `src/` — reusable prediction and evaluation code.
- `results/` — metric tables, per-language results, and confusion matrices.
- `reports/` — benchmark report and release notes.
- `docs/` — model card, training methodology, and deployment guide.

## Baseline comparison
The intended comparison includes the trained BERT-Tiny model, fast-langdetect, MIRA-IndicLID, and Sarvam Language Identification. Each model must be evaluated on the same text examples with documented label normalization and unsupported-label handling.

Important caveats from the preliminary evaluation audit:
- The supplied reference prediction export was used as a proxy ground-truth source because the original held-out dataset was not separately provided in that run. Verify the ground-truth provenance before publishing final performance claims.
- The sheet previously described as “fastText” was identified from its columns as `fast-langdetect`; it has not been verified as the original fastText `lid.176` model.
- The MIRA export contained no `en-IN` predictions in the audited file. Investigate label mapping/wrapper behavior rather than concluding the underlying model cannot detect English.
- Timing units, hardware, warm-up policy, and whether API/network time is included must be verified before treating latency as production performance.
- Very high prepared-split metrics should be checked for duplicates, template leakage, and label-policy leakage.

## Quick start
Once the checkpoint and matching tokenizer are uploaded, inference instructions will be added here.
```bash
git clone https://github.com/abhinavnautiyalDS/bert-tiny-indic-lid.git
cd bert-tiny-indic-lid
pip install -r requirements.txt
```

## Reproducibility checklist
- [ ] Upload selected checkpoint(s) and matching tokenizer files.
- [ ] Publish exact label-to-ID mapping and model configuration.
- [ ] Add fine-tuning and standalone evaluation notebooks.
- [ ] Add benchmark notebook and generated outputs.
- [ ] Document every dataset source, license, transformation, and split procedure.
- [ ] Audit train/test near-duplicates and synthetic/template leakage.
- [ ] Re-measure CPU p50/p90 latency on named hardware with warm-up and repeated runs.
- [ ] Record package versions, random seeds, and inference examples.
- [ ] Check for credentials, private data, and restricted dataset content.

## Licensing
The repository license does not override the licenses or terms of source datasets, pretrained checkpoints, or baseline systems. Choose a root license only after confirming it is compatible with all materials you plan to publish.

## Citation
Please cite this repository and the exact release/commit used. Add a versioned release and formal citation metadata when the public release is ready.