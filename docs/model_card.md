---
language: [hi, mr, bn, as, pa, gu, ta, te, kn, ml, en]
license: other
library_name: transformers
pipeline_tag: text-classification
tags: [language-identification, indic, bert, romanized, code-mixing]
datasets: [YOUR_USERNAME/YOUR_DATASET]
---
# Indic Language ID - BERT-E4

A small BERT (4 layers) fine-tuned from scratch to identify the language a text is written in: Hindi, Marathi, Bengali, Assamese, Punjabi, Gujarati, Tamil, Telugu, Kannada, Malayalam, English (India), or `none` (any other language, script, or non-linguistic text). It handles native script, romanized (Latin-script) text and code-mixed text.

## Model details
| | |
|---|---|
| Architecture | `BertForSequenceClassification`, 4 layers, hidden size 256, 4 heads, FFN 1024 |
| Parameters | about 16.1M (12.8M of them in the embedding table) |
| Vocabulary | 50,000 WordPiece, trained on the dataset's train split; lower-cased, accents kept |
| Max positions | 256 (train with max_length 192 recommended) |
| Weights | `model.safetensors`, float32, 64 MB |
| Labels | 0 hi-IN, 1 mr-IN, 2 bn-IN, 3 as-IN, 4 pa-IN, 5 gu-IN, 6 ta-IN, 7 te-IN, 8 kn-IN, 9 ml-IN, 10 en-IN, 11 none |

## Training data
Indic Language ID v6 (see its dataset card): about 958k train rows, including romanized text in many spelling styles, Devanagari dialects and other languages as `none`, and noisy / multi-sentence / fragment variants.

## Usage
```python
from transformers import pipeline
clf = pipeline("text-classification", model="PATH_OR_HUB_ID", truncation=True, max_length=192)
print(clf(["मुझे चाय पसंद है", "Aami bhat khai", "THIS IS ENGLISH!!!"]))
```
`tokenizer_config.json` does not set `model_max_length`, so always pass `truncation=True, max_length=192` (inputs over 256 tokens will otherwise fail).

## Results
Fill in after running the evaluation cell:
| Test set | Accuracy | Macro-F1 |
|---|---|---|
| v6 test split | TODO | TODO |
| v6 test, new rows only (`variant != orig`) | TODO | TODO |
| Held-out 87k evaluation set | TODO | TODO |

## Limitations
* Trained largely on synthetic, rule-generated and language-model-written text without native-speaker review.
* `none` is an open-set class learned from a limited set of languages, scripts and seeds; unseen languages may be mislabelled as a supported language.
* Weak spots found in analysis: romanized Tamil, short (1-2 word) Hindi / Marathi inputs, and Hindi vs closely related Devanagari languages (Bhojpuri, Maithili, Nepali, Sanskrit).
* Intended for language identification only, not for judging text quality or content.

## License
Set after verifying the licenses of the training data sources.
