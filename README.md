# Qwen Image FastAPI Server

This repository contains a Kaggle notebook that prepares and runs a Qwen Image generation pipeline, then exposes it through a lightweight FastAPI service for use in other apps.

The main notebook is:

- `qwen-image-quantized-model (2).ipynb`

It walks through downloading the Qwen image model, installing required runtime components, linking model files into a ComfyUI-compatible folder structure, and starting a local image-generation backend.

## What this project does

- Downloads and configures the Qwen image model for local inference
- Uses a quantized GGUF model for efficient generation
- Installs and wires in ComfyUI and required model assets
- Loads a VAE safetensors model and text encoder files
- Exposes a FastAPI endpoint that accepts a text prompt and returns generated images
- Runs the generation backend and API locally or within a Kaggle environment

## Repository structure

- `qwen-image-quantized-model (2).ipynb` — notebook that performs model setup and service orchestration
- `README.md` — project overview and usage notes

## Main workflow

The notebook performs these steps:

1. Check the environment and install required packages
2. Download or clone the required model and UI repositories
3. Download the Qwen GGUF model and supporting files
4. Link the model files into a ComfyUI `models` directory
5. Start ComfyUI or a remote tunnel for the generation backend
6. Expose a FastAPI route (`/generate`) that sends prompts to the generation service
7. Return generated images as HTTP responses

## Core technologies

- Python
- FastAPI
- ComfyUI
- GGUF / quantized model formats
- Hugging Face model downloads
- CUDA-enabled GPU environment (recommended)

## Prerequisites

- A Python environment (the notebook targets Python 3.12)
- A GPU-capable machine, ideally with CUDA support
- Sufficient RAM/VRAM for the model
- Internet access to download the model files and dependencies
- Optional: Kaggle notebook environment with persisted working storage

## Typical setup flow

1. Open the notebook in Kaggle or a local Jupyter environment.
2. Run the installation cells to install dependencies.
3. Download the model assets and place them in the expected `models` directories.
4. Start ComfyUI and confirm it is reachable.
5. Launch the FastAPI app.
6. Send a POST request to the generation endpoint with a prompt.

Example payload:

```json
{
  "prompt": "A cinematic red fox standing in a snowy forest, ultra detailed"
}
```

Example endpoint:

```bash
curl -X POST http://127.0.0.1:8000/generate \
  -H "Content-Type: application/json" \
  -d '{"prompt":"A cinematic red fox standing in a snowy forest, ultra detailed"}'
```

## Notes

- This project is designed as a local inference and API experiment rather than a polished production-ready deployment.
- Some operations depend on external model archives and ComfyUI plugins.
- The notebook includes direct shell commands and file-linking steps that may need adjustment depending on the environment.
- If running in a remote environment, ensure the public URL or tunnel endpoint is configured correctly.

## Recommended usage

Use this repo when you want to:

- test Qwen image generation locally
- host a simple prompt-to-image API
- experiment with quantized image models in a Kaggle environment
- integrate generated images into another application through HTTP

## License

Check the original model and dependency licenses before commercial use or redistribution.

## Disclaimer

This project depends on third-party model repositories and UI components. Model availability and download URLs may change over time, so some commands in the notebook may need to be updated to match current upstream sources.
