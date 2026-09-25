---
license: other
library_name: transformers
pipeline_tag: text-generation
base_model: deepseek-ai/deepseek-coder-1.3b-base
tags:
- gguf
- llama.cpp
- text-generation
- code
- deepseek
---

# DeepSeek-Coder 1.3B Base GGUF

[Source model](https://huggingface.co/deepseek-ai/deepseek-coder-1.3b-base) · [HF release](https://huggingface.co/ShayonSarker/DeepSeek-Coder-1.3B-Base-GGUF) · [Build hub](https://github.com/Dadhichi-Sarker-Shayon/DeepSeek-Coder-1.3B-Base-GGUF)

Pinned llama.cpp conversion of the official 1.3B base model. The previously listed `deepseek-ai/deepseek-coder-1b` repository does not exist; this release uses the official 1.3B base checkpoint.

## Formats

| File | Purpose |
|---|---|
| `DeepSeek-Coder-1.3B-Base-F16.gguf` | Reference quality |
| `DeepSeek-Coder-1.3B-Base-Q8_0.gguf` | Higher-quality compact format |
| `DeepSeek-Coder-1.3B-Base-Q4_K_M.gguf` | Smallest release format |

## Validation

WikiText-2 raw test evaluation, 8 chunks of 512 tokens. Lower perplexity is better.

| Format | PPL | Ratio to F16 |
|---|---:|---:|
| F16 | 18.0150 | Baseline |
| Q8_0 | 18.0253 | 1.0006 |
| Q4_K_M | 18.3160 | 1.0167 |

A deterministic Q4_K_M code-completion smoke test completed successfully:

```python
def add(a, b):
    return a + b
```

This is a base completion model, not an instruction-tuned assistant.

## Build

```bash
python -m pip install -r requirements-build.txt
python build_gguf.py --model-id deepseek-ai/deepseek-coder-1.3b-base
```

The builder pins llama.cpp commit `6b790a9c291b5d7af3312bbf9f0c558aa023b13e` and the upstream model revision. It does not upload or overwrite this repository.

## License

DeepSeek Coder Model License v1.0. redistribution is allowed only under the license conditions, including the use-based restrictions. `LICENSE` contains the complete terms and must accompany redistributed derivatives.
