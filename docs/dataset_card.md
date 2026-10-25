---
language: [hi, mr, bn, as, pa, gu, ta, te, kn, ml, en]
license: other
task_categories: [text-classification]
task_ids: [language-identification]
pretty_name: Indic Language ID v6 (10 Indian languages + English + other)
size_categories: [1M<n<10M]
tags: [language-identification, indic, code-mixing, romanized, transliteration, synthetic-data, hinglish]
configs:
- config_name: default
  data_files:
  - {split: train, path: train.jsonl}
  - {split: validation, path: validation.jsonl}
  - {split: test, path: test.jsonl}
---
# Indic Language ID (v6) - dataset card

## 1. Summary
Language identification for **Hindi, Marathi, Bengali, Assamese, Punjabi, Gujarati, Tamil, Telugu, Kannada, Malayalam and English (India)**, plus an open-set class **`none`** (anything else).
A text is labelled with the language it is *written in*, **whatever the script**: native script, romanized (Latin script) or code-mixed with English.
**1,196,795 rows** in three splits. v6 extends v5 with 292,638 rows built from an error analysis of a BERT-tiny model trained on v5.

## 2. Labels
`label_map.json`: 0 hi-IN, 1 mr-IN, 2 bn-IN, 3 as-IN, 4 pa-IN, 5 gu-IN, 6 ta-IN, 7 te-IN, 8 kn-IN, 9 ml-IN, 10 en-IN, 11 none.

## 3. Splits
| split | rows | v5 rows (`variant=orig`) | v6 rows (new) |
|---|---|---|---|
| train | 958,026 | 723,479 | 234,547 |
| validation | 119,269 | 90,219 | 29,050 |
| test | 119,500 | 90,459 | 29,041 |
| **total** | **1,196,795** | 904,157 | 292,638 |

Every derived row stays in the split of its parent row. Hand-written seeds are partitioned across splits. No identical text appears in two splits and no text carries two labels (checked in `build_report_v6.json`).

## 4. Label distribution
| label | train | validation | test | Latin-script share (train) |
|---|---|---|---|---|
| hi-IN | 82,747 | 10,404 | 10,459 | 27% |
| mr-IN | 75,678 | 9,364 | 9,452 | 18% |
| bn-IN | 75,091 | 9,565 | 9,798 | 18% |
| as-IN | 77,036 | 9,601 | 9,613 | 20% |
| pa-IN | 74,551 | 9,153 | 9,227 | 18% |
| gu-IN | 74,551 | 9,087 | 9,341 | 18% |
| ta-IN | 80,324 | 9,819 | 9,812 | 24% |
| te-IN | 74,494 | 9,330 | 9,134 | 18% |
| kn-IN | 74,570 | 9,232 | 9,153 | 18% |
| ml-IN | 77,281 | 9,708 | 9,500 | 21% |
| en-IN | 70,536 | 8,807 | 8,805 | 100% |
| none | 121,167 | 15,199 | 15,206 | 36% |

`none` is deliberately the largest class (open-set class, historically the weakest). Use class weights or down-sample via the `variant` / `language_detail` columns.

## 5. Columns
| column | meaning |
|---|---|
| `text` | the input text (may contain newlines) |
| `label`, `label_id` | class name and integer id |
| `category` | origin bucket |
| `script` | dominant script of the text (Latin, Devanagari, Bengali, Gurmukhi, Gujarati, Odia, Tamil, Telugu, Kannada, Malayalam, Arabic, Other, None) |
| `source_type` | `natural`, `synthetic`, `augmented`, `romanized_auto` |
| `language_detail` | for `none`: which language / group (odia, sanskrit, foreign_fr, other_script_armenian, numeric_id ...) |
| `variant` | `orig` for v5 rows, otherwise how the v6 row was made (section 7) |

## 6. Composition (train)
| source_type | rows | share |
|---|---|---|
| natural | 422,748 | 44.1% |
| synthetic | 199,583 | 20.8% |
| augmented | 198,534 | 20.7% |
| romanized_auto | 137,161 | 14.3% |

* `natural` - real written text (web / news style), some English-mixed.
* `synthetic` - template-generated call-centre style turns, names, backchannels, numbers/ids, and the v6 seed-based `none` text.
* `augmented` - noisy / wrapped / multi-sentence / fragment versions of existing rows.
* `romanized_auto` - machine-romanized copies of native-script rows. **Not human chat text.**

| script | rows | share |
|---|---|---|
| Latin | 269,383 | 28.1% |
| Devanagari | 146,242 | 15.3% |
| Bengali | 126,496 | 13.2% |
| Gurmukhi | 61,334 | 6.4% |
| Kannada | 61,085 | 6.4% |
| Malayalam | 60,962 | 6.4% |
| Tamil | 60,845 | 6.4% |
| Gujarati | 60,836 | 6.4% |
| Telugu | 60,695 | 6.3% |
| Odia | 20,235 | 2.1% |
| None | 14,388 | 1.5% |
| Other | 10,001 | 1.0% |
| Arabic | 5,524 | 0.6% |

Latin script is 28% of train; 137,161 rows are machine-romanized.

## 7. What v6 added (train counts)
| variant | rows | description |
|---|---|---|
| `noisy_social` | 28,574 | @user prefix, #hashtag, URL, emoji, ALL-CAPS/lower-case, typos, "!?" noise (all labels) |
| `multi_sentence` | 24,600 | 2-4 same-label sentences concatenated (space / no space / newline), up to ~150 words (all labels) |
| `misc_wrapped` | 18,300 | numeric or bracket wrappers such as "(6) ", "Rs. 1132 - ", "Fig. 3:", trailing "[12]" / "pp 30-45" (all labels) |
| `seed_splice` | 16,644 | strings spliced from hand-written Sanskrit, Meitei and 31 foreign-language seed sentences -> none |
| `roman_itrans` | 15,391 | romanized, ITRANS-like capitals (T, D, N, Sh) |
| `roman_plain` | 15,389 | romanized, schwa-retaining plain spelling |
| `dialect_rewrite` | 14,000 | Hindi rewritten with marker words of Bhojpuri / Maithili / Awadhi / Magahi / Chhattisgarhi / Nepali / Kashmiri(Devanagari) -> none |
| `roman_plain1` | 12,598 | romanized, plain spelling with single-letter long vowels |
| `roman_simple` | 9,791 | romanized, simplified spelling with final schwa deletion |
| `roman_codemix_en` | 9,397 | romanized text interleaved with English clauses |
| `short_fragment_exclusive` | 8,965 | 1-4 word fragments containing words exclusive to hi vs mr or bn vs as |
| `short_fragment` | 8,618 | 1-4 word fragments (ta/te/kn/ml/gu/pa/en) |
| `random_script` | 7,916 | random characters from 36 other Unicode scripts (Ol Chiki separate) -> none |
| `roman_dialect` | 5,745 | romanized dialect rewrites -> none |
| `roman_kn_like` | 5,556 | romanized, Kannada/Telugu-like full-vowel spelling |
| `roman_chat_sms` | 4,494 | Hinglish SMS style (nhi, muje, thk, krna) |
| `roman_chat_noise` | 4,485 | romanized with random vowel dropping (non-Hindi languages) |
| `roman_voiced2` | 4,200 | Tamil/Malayalam romanization with voicing and doubled stops (gg, dd, bb) |
| `roman_voiced` | 4,200 | Tamil/Malayalam romanization with intervocalic voicing |
| `roman_bnj` | 4,197 | Bengali-style romanization (sh, j, ng, o-endings) |
| `emoji_punct_only` | 2,501 | emoji-only or punctuation-only text -> none |
| `roman_template` | 2,500 | romanized Nepali/Sanskrit/Maithili/Bhojpuri/Konkani templates -> none |
| `roman_seed` | 1,789 | romanized Sanskrit seed splices -> none |
| `english_single_word` | 1,610 | single common English words -> en-IN |
| `random_olchiki` | 1,500 | random Ol Chiki (Santali) text -> none |
| `roman_asx` | 1,400 | Assamese-style romanization (x for sh/s, z for j) |
| `seed_sentence` | 187 | the hand-written seed sentences themselves -> none |

## 8. The `none` class (train, 121,167 rows)
| Group | Rows | Details |
|---|---|---|
| Odia (natural text) | 26,814 | native-script Odia, plus romanized Odia in the v6 rows |
| Other Indian languages | 52,229 | Sanskrit, Nepali, Maithili, Bhojpuri, Chhattisgarhi, Awadhi, Magahi, Konkani, Kashmiri (Devanagari), Sindhi, Urdu, Meitei (Bengali script), Santali (Ol Chiki) |
| Foreign Latin-script languages | 10,522 | 31 languages with hand-written seeds (fr, es, de, pt, it, nl, id, sw, tr, pl, vi, sv, tl, cy, zu, xh, ha, eo, la, fi, cs, ro, hu, da, nn, lv, mg, tn, rw, yo, so) plus 456 generic rows |
| Other scripts | 8,695 | 36 scripts (random characters per Unicode block) plus 278 generic rows |
| Numbers / IDs / codes | 18,504 | numeric ids, phone numbers, codes, emails, urls |
| Emoji / punctuation only | 2,501 | |
| Names / acronyms / entities | 1,902 | names, places, brands, spelled acronyms, entity pairs |

## 9. Text length (train)
Words: mean 14.2, median 12, p95 30, p99 49, max 129. Characters: mean 99.4, p95 215, max 995. Rows with 1-2 words: 3.94%.
A `max_length` of 192 tokens or more is recommended (multi-sentence rows reach about 130 words).

## 10. Recommended use
* Train a tokenizer that covers Indic scripts (multilingual or Indic WordPiece vocabulary); an English-only vocabulary turns Indic text into `[UNK]`.
* Use mild class weights (e.g. square-root inverse frequency).
* Numeric / ID / code rows labelled `none` (about 18,504 in train) are Latin-script and non-linguistic; drop or keep them depending on whether your application needs them.
* Do not rely on the validation split alone: it is easy (a linear char n-gram model reaches about 99.6%). Keep an external hard test set.

## 11. How it was built
Rule-based romanizer with 9 spelling schemes (plain, plain1, itrans, simple, bnj, asx, voiced, voiced2, kn_like); Hinglish SMS-style respelling; English code-mix interleaving; Hindi-to-dialect rewriting with marker words; hand-written seed sentences (Sanskrit, Meitei, 31 foreign languages) expanded by chunk splicing; random-character strings for unseen scripts; wrapper / noise / multi-sentence / fragment augmentation for every label. Scripts are in `changes_v6/` and regenerate the data from v5.

## 12. Evaluation notes
* Sanity check with a char n-gram linear model (not a neural model) on a private set of 11,315 rows that a BERT-tiny trained on v5 had misclassified: accuracy 17.2% with v5 data and 69.4% with v6 data; original validation 99.59% -> 99.56%. Weakest after v6: romanized Tamil and short Hindi / Marathi fragments.
* Treat these numbers as indicative only; they are not a benchmark of the dataset.

## 13. Known limitations and biases
* **Not human-reviewed.** Synthetic text (dialect rewrites, seeds, romanizations, random-script strings, and the language-model-written v5 text) has no native-speaker review.
* **Dialect rows are Hindi with swapped marker words**; they teach the markers, not the full languages (Bhojpuri, Maithili, Awadhi, Magahi, Chhattisgarhi, Nepali, Kashmiri).
* **Random-script rows** only teach "this script is not one of the 11".
* **Small foreign-language coverage:** 31 Latin-script languages with about 7 seed sentences each; ~170 other languages are absent.
* **Close languages:** Hindi vs Devanagari dialects / Nepali / Sanskrit / Marathi, Assamese vs Bengali, romanized Hindi vs romanized Urdu (Roman Urdu is intentionally not a `none` class).
* **Romanization is rule-based** and does not follow real users' spelling habits; real chat text will differ.
* **Short inputs** (1-2 words) are inherently ambiguous, especially Hindi / Marathi.
* **Coverage gaps:** Dogri, Bodo, Tulu, Rajasthani and many other Indian languages are not represented as separate classes.

## 14. Provenance and license
`natural` rows come from third-party corpora; verify the original licenses before publishing and set `license` accordingly. Synthetic rows were generated by rules or written by a language model.

## 15. Loading
```python
from datasets import load_dataset
ds = load_dataset("YOUR_USERNAME/YOUR_DATASET")
import pandas as pd
df = pd.read_csv("train.csv", keep_default_na=False)   # texts like "na" / "None" are valid rows
```

## 16. Version history
* v5: 904,157 rows. Language-by-writing labels, romanized rows, generated unsupported languages, Odia text.
* v6: 1,196,795 rows. Multi-scheme romanization, dialect / script / foreign-language `none` rows, noise / wrapper / multi-sentence / fragment variants, new `variant` column.
