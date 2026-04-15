# Nexus Wheels

Pre-compiled Python wheels for [flash-attn](https://github.com/Dao-AILab/flash-attention) and [vllm](https://github.com/vllm-project/vllm), built for the UMIACS Nexus cluster.

The Nexus cluster runs an older glibc (2.28), which makes installing these packages from PyPI difficult or impossible. These wheels are compiled against:

- **CUDA 12.8.1**
- **PyTorch 2.9.1**
- **Python 3.10**

## Wheels

Download from the [v1.0 release](https://github.com/minghui-liu/nexus_wheels/releases/tag/v1.0):

| Package | Download |
|---------|----------|
| flash-attn 2.8.3 | [flash_attn-2.8.3.cu128torch2.9-cp310-cp310-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl](https://github.com/minghui-liu/nexus_wheels/releases/download/v1.0/flash_attn-2.8.3.cu128torch2.9-cp310-cp310-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl) |
| vllm 0.15.1 | [vllm-0.15.1.cu128-cp310-cp310-linux_x86_64.whl](https://github.com/minghui-liu/nexus_wheels/releases/download/v1.0/vllm-0.15.1.cu128-cp310-cp310-linux_x86_64.whl) |

## Prerequisites

Load the CUDA 12.8.1 module before creating your environment or installing packages:

```bash
module load cuda/12.8.1
```

---

## Installation Instructions

Define the wheel URLs once, then use them in any of the options below:

```bash
FLASH_ATTN_WHL="https://github.com/minghui-liu/nexus_wheels/releases/download/v1.0/flash_attn-2.8.3.cu128torch2.9-cp310-cp310-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl"
VLLM_WHL="https://github.com/minghui-liu/nexus_wheels/releases/download/v1.0/vllm-0.15.1.cu128-cp310-cp310-linux_x86_64.whl"
```

### Option 1: conda

```bash
# Create and activate a conda environment with Python 3.10
conda create -n myenv python=3.10 -y
conda activate myenv

# Install PyTorch 2.9.1 with CUDA 12.8 support
pip install torch==2.9.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128

# Install flash-attn and vllm directly from the release
pip install "$FLASH_ATTN_WHL"
pip install "$VLLM_WHL"
```

---

### Option 2: venv

```bash
# Create and activate a virtual environment (must use Python 3.10)
python3.10 -m venv myenv
source myenv/bin/activate

# Install PyTorch 2.9.1 with CUDA 12.8 support
pip install torch==2.9.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128

# Install flash-attn and vllm directly from the release
pip install "$FLASH_ATTN_WHL"
pip install "$VLLM_WHL"
```

---

### Option 3: uv

```bash
# Create and activate a uv virtual environment with Python 3.10
uv venv myenv --python 3.10
source myenv/bin/activate

# Install PyTorch 2.9.1 with CUDA 12.8 support
uv pip install torch==2.9.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128

# Install flash-attn and vllm directly from the release
uv pip install "$FLASH_ATTN_WHL"
uv pip install "$VLLM_WHL"
```

---

## Notes

- These wheels are only compatible with **Python 3.10**. Make sure your environment uses Python 3.10.
- Always run `module load cuda/12.8.1` before activating your environment or running any GPU workloads.
- The wheels are compatible with PyTorch 2.9 and CUDA 12.8.
