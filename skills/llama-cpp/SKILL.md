---
name: llama-cpp
description: "llama.cpp: Local LLM inference with GGUF models."
version: 1.0.0
---

# llama.cpp

Local LLM inference using GGUF format models.

## Setup

```bash
# Build llama.cpp
cmake -B build
cmake --build build

# Download GGUF model
# From HuggingFace or other sources
```

## Usage

```python
from llama_cpp import Llama

llm = Llama("model.gguf")
response = llm("Prompt here")
```

## GGUF Models

Quantized models in GGUF format for efficient local inference.
