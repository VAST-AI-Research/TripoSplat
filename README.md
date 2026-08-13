# TripoSplat
TripoSplat converts a single 2D image into high-quality and variable number of 3D Gaussians, developed by [TripoAI](https://www.tripo3d.ai/). It can serve as a powerful pipeline tool for asset creation, AR/VR, game development, simulation environments, and beyond. This is the inference-only repo for TripoSplat. For the training code, see [TripoSplat-Training](https://github.com/runjie-yan/TripoSplat-Training).

<a href="https://arxiv.org/abs/2605.16355"><img src="https://img.shields.io/badge/Read%20Paper-B31B1B?style=for-the-badge&logo=arxiv" alt="Paper"></a>
<a href="https://www.tripo3d.ai/research/triposplat"><img src="https://img.shields.io/badge/Technical%20Blog-grey?style=for-the-badge&logo=data:image/svg%2bxml;base64,PHN2ZyB3aWR0aD0iNjUiIGhlaWdodD0iNjUiIHZpZXdCb3g9IjAgMCA2NSA2NSIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTkuNDk5MSA5LjYzNDc3TDE2LjQzNzQgMjEuNDU1NkMxNi40MzkzIDIxLjQ1ODkgMTYuNDQxMiAyMS40NjIyIDE2LjQ0MzEgMjEuNDY1NUwzMC4yNjU4IDQ1LjA1NDhDMzEuNTMyNyA0Ny4yMTY3IDM0LjcwNDUgNDcuMjE2NyAzNS45NzE0IDQ1LjA1NDhMNDkuMzg2MiAyMi4xNjE2SDU5LjQ2MThMNDEuMjY2IDUzLjE2MkMzNy42NDQ5IDU5LjMzMTMgMjguNTkyMyA1OS4zMzEzIDI0Ljk3MTIgNTMuMTYyTDYuNjM5NjcgMjEuOTMwMkM0LjAyNCAxNy40NzM5IDUuNjU5NTYgMTIuMjEyNyA5LjQ5OTEgOS42MzQ3N1oiIGZpbGw9IndoaXRlIi8+CjxwYXRoIGQ9Ik0yMC4xMTIxIDE2LjYwODdIMzQuNjkyNkwyOC42MjIgMjcuMDQ0MkMyOC4yMDMzIDI3Ljc2NCAyOC4yMDgzIDI4LjY0OTIgMjguNjM1MSAyOS4zNjQ0TDMxLjA1MjcgMzMuNDE1MUMzMS45NjU0IDM0Ljk0NDUgMzQuMjE2MyAzNC45MzY1IDM1LjExNzggMzMuNDAwNkw0NC45NzM5IDE2LjYwODdINDYuOTQyTDQ2Ljk0NTUgMTYuNjA4N0g2MC44NDQ2QzYwLjQ4MzIgMTIuMDU4NyA1Ni42NzMxIDguMDQ4ODMgNTEuNDUwOSA4LjA0ODgzTDE1LjA4NzkgOC4wNDg4M0wyMC4xMTIxIDE2LjYwODdaIiBmaWxsPSIjRjhDRjAwIi8+Cjwvc3ZnPgo=" alt="Technical Blog"></a>
<a href="https://huggingface.co/spaces/VAST-AI/TripoSplat"><img src="https://img.shields.io/badge/Huggingface%20Demo-grey?style=for-the-badge&logo=huggingface" alt="HuggingFace Demo"></a>

| ![](static/doc/001.webp) | ![](static/doc/002.webp) |
|---|---|
| ![](static/doc/003.webp) | ![](static/doc/004.webp) |

## Highlights
- **High-quality, versatile generation** that handles a wide range of image styles.
- **Arbitrary Gaussian count** (up to 262,144) — trade off visual quality against rendering cost according to your need.
- **Minimal, readable code**: two files (`triposplat.py` and `model.py`), ~2,000 LOC total. Easy to customize and integrate into other ecosystems.
- **Near-zero dependencies**: no `transformers`, no `diffusers`, no version-conflict hell. Runs on any platform.
- **Official ComfyUI support**: drop the [official workflow template](https://github.com/Comfy-Org/workflow_templates/blob/main/templates/3d_triposplat_image_to_gaussian_splat.json) into ComfyUI and start playing with TripoSplat right away.

## Quickstart
Download model weights to `ckpts/` from [HuggingFace](https://huggingface.co/VAST-AI/TripoSplat). 
```bash
# Use one of the following ways to download model weights.

# 1. Use HuggingFace CLI
hf download VAST-AI/TripoSplat --local-dir ckpts/

# 2. Use huggingface_hub
pip install huggingface_hub
python -c "from huggingface_hub import snapshot_download; snapshot_download(repo_id='VAST-AI/TripoSplat', local_dir='ckpts/')"

# 3. Use ModelScope CLI
pip install modelscope
modelscope download VAST-AI-Research/TripoSplat --local_dir ckpts/

# 4. Use modelscope Python SDK
pip install modelscope
python -c "from modelscope import snapshot_download; snapshot_download('VAST-AI-Research/TripoSplat', local_dir='ckpts/')"

# 5. Manual download from HuggingFace / ModelScope.
```

Setup the environment and run the example inference script.
```bash
# install torch and torchvision according to your environment
pip install numpy safetensors pillow tqdm
python run_example.py
```

The exported `.ply` / `.splat` files can be visualized in any 3D Gaussian
viewer — e.g. [SparkJS](https://sparkjs.dev) or
[SuperSplat](https://superspl.at/editor).


## Gradio Demo

```bash
pip install gradio
python run_gradio.py
```

## License
TripoSplat code and weight models are released under the [MIT License](https://github.com/VAST-AI-Research/TripoSplat/blob/main/LICENSE).

## Citation
If you find TripoSplat useful, please cite:
```bibtex
@misc{yan2026generative3dgaussianslearned,
    title={Generative 3D Gaussians with Learned Density Control}, 
    author={Runjie Yan and Yan-Pei Cao and Peng Wang and Ding Liang and Yuan-Chen Guo},
    year={2026},
    eprint={2605.16355},
    archivePrefix={arXiv},
    primaryClass={cs.GR},
    url={https://arxiv.org/abs/2605.16355}, 
}
```
