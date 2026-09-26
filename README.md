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
- code-completion
- 1.3b
- quantization
- q4_k_m
- q8_0
---

# DeepSeek-Coder 1.3B Base GGUF

<div align="center">

<a href="https://huggingface.co/ShayonSarker/DeepSeek-Coder-1.3B-Base-GGUF"><img alt="Hugging Face" src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge"></a>
<a href="https://github.com/Dadhichi-Sarker-Shayon/DeepSeek-Coder-1.3B-Base-GGUF"><img alt="GitHub" src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge"></a>

<img alt="Model" src="https://img.shields.io/badge/model-DeepSeek--Coder--1.3B--base-8A2BE2?style=for-the-badge">
<img alt="GGUF formats" src="https://img.shields.io/badge/GGUF-F16%20%7C%20Q8_0%20%7C%20Q4_K_M-FFD21E?style=for-the-badge">
<img alt="Task" src="https://img.shields.io/badge/task-code--completion-00A6A6?style=for-the-badge">
<img alt="Parameters" src="https://img.shields.io/badge/params-1.3B-16A34A?style=for-the-badge">
<img alt="Base model" src="https://img.shields.io/badge/type-base%20(not%20instruct)-0069B4?style=for-the-badge">
<img alt="License" src="https://img.shields.io/badge/license-DeepSeek%20Model%20License-E8590C?style=for-the-badge">

</div>

[Source model](https://huggingface.co/deepseek-ai/deepseek-coder-1.3b-base) · [HF release](https://huggingface.co/ShayonSarker/DeepSeek-Coder-1.3B-Base-GGUF) · [Build hub](https://github.com/Dadhichi-Sarker-Shayon/DeepSeek-Coder-1.3B-Base-GGUF)

Pinned llama.cpp conversion of the official 1.3B base model. The previously listed `deepseek-ai/deepseek-coder-1b` repository does not exist; this release uses the official 1.3B base checkpoint.

## Formats

| File | Status | Purpose |
|---|---|---|
| `deepseek-coder-1.3b-base-F16.gguf` | Published | Reference quality |
| `deepseek-coder-1.3b-base-Q8_0.gguf` | Published | Higher-quality compact format |
| `deepseek-coder-1.3b-base-Q4_K_M.gguf` | Published | Smallest release format |

## Verified code completions

Verbatim `deepseek-coder-1.3b-base-Q4_K_M.gguf` completions, `--temp 0`, 24 new tokens. This is the **base** checkpoint, so it continues code rather than answering instructions. The prompt is shown as the `def`/`for`/`SELECT` line plus the already-given `return` or `print(`, and the model's text is reproduced as-is.

| Prompt | Model completion |
|---|---|
| `def is_even(number):`<br>`    return` | `number % 2 == 0` |
| `def reverse_text(text):`<br>`    return` | `text[::-1]` |
| `def factorial(number):`<br>`    if number <= 1:`<br>`        return` | `1`<br>`    else:`<br>`        return number * factorial(number - 1)` |
| `def sum_list(numbers):`<br>`    return` | `sum(numbers)` |
| `def find_max(numbers):`<br>`    return` | `max(numbers)` |
| `for index, item in enumerate(items):`<br>`    print(` | `index, item)` |

Python body completions are correct in all five cases. SQL is not: `SELECT name FROM users WHERE active =` continues into unrelated JavaScript-style ORM code, and `SELECT COUNT(*) FROM orders WHERE total >` returns a bare number. The `def`-style prompts are also filled with boilerplate follow-ups such as a generated `is_odd` helper, trimmed above.

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
