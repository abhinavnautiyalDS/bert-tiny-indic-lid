# Model artifacts

Upload the selected fine-tuned checkpoint and its matching tokenizer here.

Suggested layout:
- bert-tiny-e2/ — config.json, model.safetensors or pytorch_model.bin, tokenizer files, label mapping.
- bert-tiny-e4/ — config.json, model.safetensors or pytorch_model.bin, tokenizer files, label mapping.

Before release:
1. Verify each tokenizer is the one used to train that checkpoint.
2. Include model configuration and exact label-to-ID mapping.
3. Record model size, parameter count (measured from the actual config), framework versions, and license.
4. Test a clean CPU inference example.
5. Do not upload secrets, private data, or files whose license does not permit redistribution.

If files exceed GitHub's ordinary file limit, use Git LFS or a model hosting platform such as Hugging Face Hub and link to the immutable model revision here.
