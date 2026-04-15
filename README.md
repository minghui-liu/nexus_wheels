# Nexus Wheels

Pre-compiled Python wheels for [flash-attn](https://github.com/Dao-AILab/flash-attention) and [vllm](https://github.com/vllm-project/vllm), built for the UMIACS Nexus cluster.

The Nexus cluster runs an older glibc (2.28), which makes installing these packages from PyPI difficult or impossible. These wheels are compiled against:

- **CUDA 12.8.1**
- **PyTorch >= 2.8** (2.9.1 recommended)
- **Python 3.10**

## Wheels

| Package | Wheel file |
|---------|-----------|
| flash-attn 2.8.3 | `flash_attn-2.8.3+cu12torch2.8cxx11abiTRUE-cp310-cp310-linux_x86_64.whl` |
| vllm 0.15.1 | `vllm-0.15.1+cu128-cp310-cp310-linux_x86_64.whl` |

## Prerequisites

Load the CUDA 12.8.1 module before creating your environment or installing packages:

```bash
module load cuda/12.8.1
```

---

## Installation Instructions

### Option 1: conda

```bash
# Create and activate a conda environment with Python 3.10
conda create -n myenv python=3.10 -y
conda activate myenv

# Install PyTorch 2.9.1 with CUDA 12.8 support
pip install torch==2.9.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128

# Install flash-attn and vllm from the local wheels
pip install flash_attn-2.8.3+cu12torch2.8cxx11abiTRUE-cp310-cp310-linux_x86_64.whl
pip install vllm-0.15.1+cu128-cp310-cp310-linux_x86_64.whl
```

---

### Option 2: venv

```bash
# Create and activate a virtual environment (must use Python 3.10)
python3.10 -m venv myenv
source myenv/bin/activate

# Install PyTorch 2.9.1 with CUDA 12.8 support
pip install torch==2.9.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128

# Install flash-attn and vllm from the local wheels
pip install flash_attn-2.8.3+cu12torch2.8cxx11abiTRUE-cp310-cp310-linux_x86_64.whl
pip install vllm-0.15.1+cu128-cp310-cp310-linux_x86_64.whl
```

---

### Option 3: uv

```bash
# Create and activate a uv virtual environment with Python 3.10
uv venv myenv --python 3.10
source myenv/bin/activate

# Install PyTorch 2.9.1 with CUDA 12.8 support
uv pip install torch==2.9.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128

# Install flash-attn and vllm from the local wheels
uv pip install flash_attn-2.8.3+cu12torch2.8cxx11abiTRUE-cp310-cp310-linux_x86_64.whl
uv pip install vllm-0.15.1+cu128-cp310-cp310-linux_x86_64.whl
```

---

## Notes

- These wheels are only compatible with **Python 3.10**. Make sure your environment uses Python 3.10.
- Always run `module load cuda/12.8.1` before activating your environment or running any GPU workloads.
- The wheels are built with `cxx11abi=TRUE`. If you see ABI-related errors, ensure your PyTorch installation also uses the CXX11 ABI (the default for PyPI/`whl/cu128` builds).
