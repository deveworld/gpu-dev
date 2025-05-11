# gpu-dev
A docker image environment for LLM development on GPUs (Nvidia), useful with gcube or vastai.

Include torch, [transformers](https://github.com/huggingface/transformers), [unsloth](https://github.com/unslothai/unsloth), [flash-attn](https://github.com/Dao-AILab/flash-attention), [axolotl](https://github.com/axolotl-ai-cloud/axolotl).

Use port 8000 for jupyter notebook.

## Usage
### Cuda 12.6
```
docker pull ghcr.io/deveworld/gpu-dev:cuda-12.6
```
### Cuda 12.8 (for 50XX)
```
docker pull ghcr.io/deveworld/gpu-dev:cuda-12.8
```

## Make Docker Image
Need >= 210GB RAM

### Clone
```
git clone https://github.com/deveworld/gpu-dev
```

### Build
```
sudo docker build -t ghcr.io/deveworld/gpu-dev:latest -t ghcr.io/deveworld/gpu-dev:cuda-12.6 . -f 12.6/Dockerfile
sudo docker build -t ghcr.io/deveworld/gpu-dev:cuda-12.8 . -f 12.8/Dockerfile
```

### Login
```
sudo docker login --username {username} --password-stdin
```

### Push
```
sudo docker push ghcr.io/deveworld/gpu-dev --all-tags
```
