---
name: unsloth
description: "Unsloth: fast LLM fine-tuning."
version: 1.0.0
---

# Unsloth

Fast LLM fine-tuning with Unsloth.

## Features

- 2x faster training
- 50% less memory
- Gradient checkpointing

## Usage

```python
from unsloth import FastLanguageModel
model, tokenizer = FastLanguageModel.from_pretrained("unsloth/llama-3-8b")
```
