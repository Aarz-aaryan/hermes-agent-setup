# ComfyUI — Generate Images, Video, and Audio with ComfyUI

## Setup

### 1. Install ComfyUI
```bash
git clone https://github.com/comfyanonymous/ComfyUI.git
cd ComfyUI
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.txt
```

### 2. Start ComfyUI Manager (optional but recommended)
```bash
cd custom_nodes
git clone https://github.com/ltdrdata/ComfyUI-Manager.git
```

### 3. Start ComfyUI
```bash
python main.py --listen 0.0.0.0 --port 8188
```

## Workflow File Locations
ComfyUI workflows are JSON files that define the node graph. Save them as `.json` files.

## Key Node Types

### Model Loading
- **CheckpointLoader/Simple Load器** — Load .safetensors checkpoint files
- **CLIPLoader** — Load CLIP text encoder models
- **VAELoader** — Load VAE models

### Text Encoding
- **CLIPTextEncode** — Encode positive/negative prompts to conditioning

### Sampling
- **KSampler** — Core sampling node
  - model: the model output from loader
  - seed: random seed
  - steps: number of steps
  - cfg: CFG scale (default 8)
  - sampler_name: euler, euler_ancestral, dpmpp_2m, dpmpp_sde, etc.
  - scheduler: normal, karras, exponential, simple, beta
  - positive: positive conditioning
  - negative: negative conditioning
  - latent_image: latent image to sample (or empty for generation)

### Latent/Image Conversion
- **VAEDecode** — Decode latent to image
- **VAEEncode** — Encode image to latent
- **EmptyLatentImage** — Create empty latent for generation
- **LoadImage** — Load image file
- **SaveImage** — Save image to file

### Advanced Nodes (Manager required)
- **ControlNet** — Apply ControlNet conditioning
- **ControlNet Preprocessor** — Detect edges, poses, depth from images
- **IPAdapter** — Apply image-to-image adaptation
- **InstantID** — Face-to-face identity preservation
- **AnimateDiff** — Video generation with motion LoRAs
- **DeOldify** — Colorize black and white images

## Workflow Examples

### Text-to-Image
1. CheckpointLoader → CLIPTextEncode (positive) → CLIPTextEncode (negative)
2. EmptyLatentImage → KSampler (with above conditioning)
3. KSampler → VAEDecode → SaveImage

### Image-to-Image (img2img)
1. CheckpointLoader → CLIPTextEncode (positive) → CLIPTextEncode (negative)
2. LoadImage → VAEEncode → KSampler
3. KSampler → VAEDecode → SaveImage

### Inpainting
1. LoadImage → Mask → VAEEncode (with mask)
2. CheckpointLoader → CLIPTextEncode → CLIPTextEncode
3. KSampler → VAEDecode → SaveImage

### ControlNet
1. LoadImage → ControlNet Preprocessor → ControlNet Apply
2. CheckpointLoader + ControlNet → CLIPTextEncode → KSampler
3. KSampler → VAEDecode → SaveImage

## Performance Tips
- Use `fp16` (half precision) models to save VRAM
- Use `cpu` offload if VRAM is limited: `--lowvram` or `--novnc`
- Batch size 2-4 on 24GB VRAM depending on resolution
- Use `turbo` mode in ComfyUI-Manager for faster sampling

## API Access
ComfyUI has a REST API at `http://localhost:8188`:
- `GET /history` — recent history
- `GET /history/<prompt_id>` — specific prompt history
- `POST /prompt` — queue a prompt
- `GET /system_stats` — VRAM usage

## Custom Nodes
Install via ComfyUI Manager or manually:
```bash
cd custom_nodes
git clone <repo_url>
```

## Workspace Path
User's ComfyUI is at: `~/comfyui/`
Workflows saved at: `~/comfyui/user/default/workflows/`
