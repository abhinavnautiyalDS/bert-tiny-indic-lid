# Preliminary benchmark caveats

These summary tables preserve preliminary results from the earlier evaluation audit; they are not a final model card or independently re-run release benchmark.

- The full-set reference labels came from a supplied MIRA prediction export because the original held-out ground-truth dataset was not separately supplied for that benchmark run. Confirm the source and label validity before making performance claims.
- The supplied file described as fastText was identified from its columns as fast-langdetect. It is not confirmed to be the original fastText lid.176 implementation.
- The MIRA export contained no en-IN predictions. Investigate output mapping/wrapper configuration; do not infer that the underlying model cannot identify English.
- The Sarvam paired subset contained 3,952 rows. The timing values for Sarvam and the local models use unverified units/protocols, so do not present them as apples-to-apples production latency.
- Reported values are coverage, supported-prediction accuracy, operational accuracy, balanced accuracy, macro-F1, weighted-F1 as available. Confirm definitions in the notebook before comparing them with other publications.
- Prepared-test scores can be inflated by duplicate or template leakage. Re-audit near-duplicates, source overlap, and label policy.
- Before public release, rerun evaluation from the exact dataset split with fixed label mapping, hardware, warm-up policy, batch size, timing units, and dependency versions.
