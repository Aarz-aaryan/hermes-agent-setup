---
name: huggingface-hub
description: "HuggingFace Hub: model and dataset access."
version: 1.0.0
---

# HuggingFace Hub

Access HuggingFace models and datasets.

## Setup

```python
from huggingface_hub import snapshot_download
model_path = snapshot_download("meta-llama/Llama-3-8b")
```

## Operations

- Download models
- Upload models
- List datasets
