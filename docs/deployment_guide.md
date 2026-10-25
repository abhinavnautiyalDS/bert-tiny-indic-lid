# Deployment guide

Deployment instructions will be finalized after the checkpoint and tokenizer are included.

For a production evaluation:
1. Load the exact checkpoint and tokenizer in a clean environment.
2. Run CPU warm-up iterations and repeated measurements at realistic transcript lengths.
3. Report p50/p90/p95 latency, throughput, peak memory, and model/tokenizer disk size.
4. Include preprocessing and postprocessing costs, but report network/API time separately.
5. Test short greetings, backchannels, transliterated text, code-switching, ASR errors, names/entities, and unsupported languages.
6. Keep language classification separate from the voice agent's switching policy; a single uncertain turn should not automatically force a language switch without a defined policy.
