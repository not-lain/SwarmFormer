# SwarmFormer

A novel transformer architecture for sentiment analysis that combines local swarm intelligence with global attention mechanisms.

## Features

- Efficient local-global information processing
- Hierarchical clustering of tokens
- Dynamic gating mechanisms with GELU activations
- Comprehensive dropout strategy (0.3-0.4)
- State-of-the-art performance on sentiment analysis

## Installation

### Prerequisites

- Python >= 3.8
- PyTorch >= 2.0.0
- CUDA (optional, but recommended for GPU acceleration)

### Quick Install

You can install the package directly from the repository:

```bash
# Clone the repository
git clone https://github.com/takara-ai/SwarmFormer.git
cd SwarmFormer

# Create and activate a virtual environment (recommended)
python -m venv .venv
source .venv/bin/activate  # On Windows, use `.venv\Scripts\activate`

# Install the package in editable mode with all dependencies
pip install -e .
```

## Demo

### Running the Demo Script

The package includes a demo script that runs inference on the IMDb dataset:

```bash
# Run with base model (default)
python run_inference.py

# Run with small model
python run_inference.py --model-size small
```

The demo will:

1. Download the pre-trained model from HuggingFace automatically
2. Load the IMDb test dataset
3. Run inference and display:
   - Model architecture details
   - Parameter counts
   - Accuracy metrics
   - Latency statistics
   - Throughput measurements

### Using in Your Code

```python
from swarmformer.config import MODEL_CONFIGS
from swarmformer.inference import load_trained_model, evaluate_model, get_device

# Get configuration and device
config = MODEL_CONFIGS['base']  # or 'small'
device = get_device()

# Load model
model, dataset = load_trained_model(config, device)

# Run inference
metrics = evaluate_model(model, dataset, batch_size=256, device=device)
print(f"Accuracy: {metrics['accuracy']:.4f}")
```

# HuggingFace Integration

SwarmFormer now integrates seamlessly with the HuggingFace ecosystem, providing the following methods:

```python
# Save model to local directory
model.save_pretrained("path/to/save")

# Load model from local directory or HuggingFace Hub
model = SwarmFormer.from_pretrained("takara-ai/swarmformer-base")

# Push your fine-tuned model to HuggingFace Hub
model.push_to_hub("your-username/your-model-name")
```

For detailed instructions on HuggingFace integration, see our [PR #2](https://github.com/takara-ai/SwarmFormer/pull/2).

## Model Configurations

The package includes two pre-trained model configurations:

### SwarmFormer-Base

- **Architecture**:

  - Embedding dimension: 192
  - Number of layers: 2
  - Local update steps: 3
  - Cluster size: 4
  - Sequence length: 768
  - Comprehensive dropout (0.3-0.4)

- **Performance**:
  - Accuracy: 89.03%
  - Precision: 87.22%
  - Recall: 91.46%
  - F1: 89.29%
  - Mean batch latency: 4.83ms
  - Peak memory: 9.13GB

### SwarmFormer-Small

- **Architecture**:

  - Embedding dimension: 128
  - Number of layers: 2
  - Local update steps: 3
  - Cluster size: 8
  - Sequence length: 256
  - Optimized dropout (0.3)

- **Performance**:
  - Accuracy: 86.20%
  - Precision: 83.46%
  - Recall: 90.31%
  - F1: 86.75%
  - Inference time: 0.36s (25k samples)
  - Mean batch latency: 3.67ms
  - Throughput: 45k samples/s
  - Peak memory: 8GB

## Hardware Support

The package automatically selects the best available hardware:

- NVIDIA CUDA GPUs (recommended, tested on RTX 2080 Ti)
- Apple Silicon (M1/M2) via MPS
- CPU (fallback)

## Requirements

All dependencies are automatically installed with the package:

- Python >= 3.8
- PyTorch >= 2.0.0
- Transformers >= 4.0.0
- And others listed in requirements.txt

## Limitations

- SwarmFormer-Small: Not suitable for sequences >256 tokens
- SwarmFormer-Base: Not suitable for sequences >768 tokens
- English text classification only
- Not designed for:
  - Text generation
  - Machine translation
  - Real-time processing without adequate hardware

## Citation

If you use this code in your research, please cite:

```bibtex
@article{legg2025swarmformer,
  title={SwarmFormer: Local-Global Hierarchical Attention via Swarming Token Representations},
  author={Legg, Jordan and Sturmanis, Mikus and {Takara.ai}},
  journal={Takara.ai Research},
  year={2025},
  url={https://takara.ai/papers/SwarmFormer-Local-Global-Hierarchical-Attention-via-Swarming-Token-Representations.pdf}
}
```

## Contact

For questions, collaborations, or other inquiries:

- Email: research@takara.ai
- Repository: https://github.com/takara-ai/SwarmFormer
