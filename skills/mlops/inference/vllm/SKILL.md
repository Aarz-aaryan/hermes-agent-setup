---
name: vllm
description: "vLLM: high-throughput LLM inference."
version: 1.0.0
---

# vLLM

High-throughput LLM inference engine.

## Setup

```bash
pip install vllm
```

## Usage

```python
from vllm import LLM
llm = LLM("meta-llama/Llama-3-8B")
```

## Features

- PagedAttention
- Tensor parallelism
- Streaming output
