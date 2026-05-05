---
name: llama-cpp-inference
description: "llama.cpp inference for local LLMs."
version: 1.0.0
---

# llama.cpp Inference

Local LLM inference using llama.cpp.

## Setup

```bash
# Build llama.cpp
cmake -B build && cmake --build build
```

## Run

```bash
./build/bin/llama-server -m model.gguf -c 4096
```
