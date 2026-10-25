# Model card: BERT-Tiny Indic LID

## Model overview
A fine-tuned BERT-Tiny sequence classifier intended for text-based identification of Indian languages, including use in latency-sensitive voice-agent pipelines.

## Intended use
Language identification for text snippets and speech-recognition transcripts. Evaluate separately on short greetings, Romanized text, code-mixed utterances, ASR errors, names/entities, and unsupported languages before deployment.

## Labels
The current target label set is: as-IN, bn-IN, en-IN, gu-IN, hi-IN, kn-IN, ml-IN, mr-IN, none, pa-IN, ta-IN, te-IN. See the dataset card for exact label semantics.

## Architecture and training
To be completed from the actual checkpoint and training notebook: model configuration, tokenizer, number of parameters, training hyperparameters, dataset revision, seed, and compute environment.

## Evaluation
Add final held-out metrics, per-language results, confusion matrices, calibration/coverage analysis, and CPU p50/p90 latency after rerunning with a documented protocol.

## Limitations
Do not assume high prepared-split scores imply real-world generalization. Audit duplicate/template leakage, short and ambiguous utterances, code-switching, transliteration, ASR noise, domain shift, and unsupported languages.

## Licensing and ethics
Document the model/checkpoint license and all training-data source terms before release. Do not include private call transcripts or credentials.
