Here's an improved version with detailed steps, proper markdown formatting, and clear instructions:

---

# Langchain-Transformers-Python

This guide walks you through setting up a Python environment, installing dependencies, configuring GPU usage, and running a transformer model with LangChain.

---

## 1. Create a Virtual Environment

Creating a virtual environment helps isolate dependencies and prevents conflicts with other Python projects.

### **For Windows (Command Prompt)**
```sh
python -m venv langchain-env
langchain-env\Scripts\activate
```

### **For macOS/Linux (Terminal)**
```sh
python -m venv langchain-env
source langchain-env/bin/activate
```

---

## 2. Install Requirements

Once the virtual environment is activated, install the required dependencies.

```sh
pip install langchain transformers langchain-huggingface
```

---

## 3. Configure GPU Usage

If you have an NVIDIA GPU, install the CUDA-enabled version of PyTorch.

Run the following command (replacing `cu126` with your CUDA version):

```sh
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126
```

To check which CUDA version you have installed, run:

```sh
nvcc --version
```

If you don’t have CUDA installed, follow the official installation guide:  
🔗 [CUDA Installation Guide](https://developer.nvidia.com/cuda-downloads)

---

## 4. Check for GPU Availability

Run the following Python code to verify that your GPU is available:

```python
import torch

# Check if GPU is available
gpu_available = torch.cuda.is_available()
device_name = torch.cuda.get_device_name(0) if gpu_available else "No GPU found"

print(f"GPU Available: {gpu_available}")
print(f"GPU Name: {device_name}")
```

If `torch.cuda.is_available()` returns `False`, ensure that:
- You have an NVIDIA GPU.
- The correct version of CUDA is installed.
- You installed the CUDA-enabled version of PyTorch.

---

## 5. Set Device in Pipeline

Once GPU availability is confirmed, specify the device in the transformer pipeline.

```python
from transformers import pipeline

# Load the model and set device to GPU (device=0)
model = pipeline(
    "text-generation",
    model="mistralai/Mistral-7B-Instruct-v0.1",
    device=0  # Use GPU (0 refers to the first GPU)
)

# Generate text
output = model("What is LangChain?")
print(output)
```

If using a CPU instead of a GPU, change `device=0` to `device=-1`.

---

## 🎯 Summary

| Step                     | Command / Code |
|--------------------------|------------------------------------------------|
| **Create a Virtual Env** | `python -m venv langchain-env && source langchain-env/bin/activate` |
| **Install Requirements** | `pip install langchain transformers langchain-huggingface` |
| **Install GPU Support**  | `pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126` |
| **Check GPU Availability** | `print(torch.cuda.is_available())` |
| **Run Model on GPU** | `pipeline("text-generation", model="mistralai/Mistral-7B-Instruct-v0.1", device=0)` |

---

Now you’re ready to use **LangChain and Transformers** with GPU acceleration! 🚀
