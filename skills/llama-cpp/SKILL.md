# Llama.cpp — Local GGUF Inference + HF Hub Discovery

## Concept
llama.cpp provides fast CPU (and GPU) inference for GGUF quantized models. It's the backbone for most local LLM setups.

## Setup

### 1. Build llama.cpp
```bash
git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp
mkdir build && cd build
cmake .. -DLLAMA_CUBLAS=ON  # for GPU support
cmake --build . --config Release
```

### 2. Download a GGUF model
```bash
# From HuggingFace via hf-cli
hf-cli download --token YOUR_TOKEN \
  --include "*.gguf" \
  --repo-type model \
  "meta-llama/Llama-3.1-8B-Instruct-GGUF"
```

Or use `modelscope`:
```bash
modelscope download --model_id meta-llama/Llama-3.1-8B-Instruct-GGUF --local_dir ./models
```

### 3. Run inference
```bash
./build/bin/llama-server \
  -m models/llama-3.1-8b-instruct-q4_k_m.gguf \
  -c 4096 \
  --host 0.0.0.0 \
  --port 8080
```

## Common Tools

### llama-cli (interactive CLI)
```bash
./build/bin/llama-cli \
  -m models/model.gguf \
  -p "You are a helpful assistant." \
  -n 512 \
  --temp 0.7 \
  -t 8
```

### llama-server (HTTP server)
```bash
./build/bin/llama-server -m model.gguf -c 4096 --port 8080
# Then query:
curl http://localhost:8080/completion \
  -d '{"prompt": "Hello!", "n_predict": 128}'
```

### llama-bench
```bash
./build/bin/llama-bench -m model.gguf -ngl 99 -t 8
```

### llama-eval (offline batch evaluation)
```bash
./build/bin/llama-eval -m model.gguf -f prompts.txt
```

### llama-imatrix (importance matrix for calibration)
```bash
./build/bin/llama-imatrix -m model.gguf -f corpus.txt
```

## Quantization Types

| Type | Size | Quality | Speed |
|------|------|---------|-------|
| Q2_K | ~60% | High | Medium |
| Q3_K_M | ~70% | Good | Medium |
| Q4_0 | ~75% | Good | Fast |
| Q4_K_M | ~80% | Great | Fast |
| Q5_0 | ~85% | Great | Medium |
| Q5_K_M | ~87% | Excellent | Medium |
| Q6_K | ~90% | Excellent | Medium |
| Q8_0 | ~100% | Near-perfect | Slow |

**Recommended:** Q4_K_M or Q5_K_M for balance of speed and quality.

## GPU Support

### CUDA (NVIDIA)
```bash
cmake .. -DLLAMA_CUBLAS=ON -DCUDA_CUBLAS=ON
# Use: -ngl 99 (number of layers to offload to GPU)
./llama-server -m model.gguf -ngl 99
```

### HIP (AMD)
```bash
cmake .. -DLLAMA_HIPBLAS=ON -DAMDGPU_TARGETS=gfx1100
```

### Metal (Apple Silicon)
```bash
cmake .. -DLLAMA_METAL=ON
./llama-server -m model.gguf -ngl 999
```

## HuggingFace Hub Integration

### Search for GGUF models
```python
from huggingface_hub import list_models

models = list(list_models(
    model_name="llama",
    sort="downloads",
    direction=-1,
    filter="gguf"
))
for m in models[:10]:
    print(m.id, m.downloads)
```

### Download specific file
```python
from huggingface_hub import hf_hub_download

path = hf_hub_download(
    repo_id="meta-llama/Llama-3.1-8B-Instruct-GGUF",
    filename="llama-3.1-8b-instruct-q4_k_m.gguf",
    token="YOUR_TOKEN"
)
```

## Server API (llama-server)

### Completion endpoint
```bash
curl http://localhost:8080/completion \
  -d '{"prompt": "[INST] <<SYS>><</SYS>>Hello! <<ASST>><</ASST>>",
       "n_predict": 256,
       "temperature": 0.7,
       "stop": ["</s>", "[INST]"]}'
```

### Chat completion (with prompt format)
```bash
curl http://localhost:8080/completion \
  -d '{"prompt": "<|begin_of_text|><|start_header_id|>user<|end_header_id|>\n\nHello<|eot_id|>\n<|start_header_id|>assistant<|end_header_id|>\n\n",
       "n_predict": 256,
       "temperature": 0.7}'
```

## Workspace Path
User's llama.cpp is at: `~/llama.cpp/`
Models are at: `~/models/`
