---
layout: page
title: PyTorch to LiteRT Conversion
slim: true
cover-img: images/tutorial_photos/pytorch_litert.png
---

# PyTorch to LiteRT

## Table of Contents
- [The `litert_torch` Version](#the-litert_torch-version)
    - [Setup](#setup)
    - [1) Load PyTorch model](#1-load-pytorch-model)
    - [2) Convert PyTorch -> LiteRT](#2-convert-pytorch---litert)
    - [3) Final check](#3-final-check)
- [The ONNX Version (Deprecated)](#the-onnx-version-deprecated)
    - [Setup](#setup-1)
    - [1) Load PyTorch model](#1-load-pytorch-model-1)
    - [2) Export PyTorch -> ONNX](#2-export-pytorch---onnx)
    - [3) Convert ONNX -> TensorFlow SavedModel](#3-convert-onnx---tensorflow-savedmodel)
    - [4) Convert SavedModel -> LiteRT](#4-convert-savedmodel---litert)
    - [5) Final check](#5-final-check)

## The `litert_torch` Version

This notebook converts a PyTorch model directly into a LiteRT `.tflite` file.

1. Load the PyTorch model
2. Convert it with `litert_torch`
3. Export the generated `.tflite` file

> NOTE: This code is also available in the repository, specifically `notebooks/model_conversion/pytorch_to_litert.ipynb`.

### Setup

Install the dependencies in your python environment first, it is recommended to use a separate virtual environment for this notebook compared to the one used to install the dependencies of `requirements.txt` since some of these have specific version requirements that may conflict with the ones found there.

Especifically since `litert_torch` requires `torch==2.6.0` or greater, which differs with the version required by `requirements.txt`.

```bash
%pip install --upgrade torch torchvision litert_torch jupyter ipykernel
```

Run to check that the dependencies are correctly installed.

```python
from pathlib import Path

import torch

from torchvision.models import mobilenet_v2
from ai_edge_litert import interpreter as litert_interpreter
import litert_torch

print("Active PyTorch version:", torch.__version__)
```

```python
ARTIFACTS_DIR = Path('artifacts')
ARTIFACTS_DIR.mkdir(parents=True, exist_ok=True)

WEIGHTS_PATH = ARTIFACTS_DIR / 'mobilenet_v2_best_model.pth'
TFLITE_PATH = ARTIFACTS_DIR / 'mobilenet_v2_litert.tflite'

print('Artifacts dir:', ARTIFACTS_DIR)
```

This `artifacts` directory is where the generated `.tflite` file will be saved, as well as where you can put your PyTorch model weights to be converted.

### 1) Load PyTorch model

Here we load the PyTorch model and extract the number of classes from the final layer, in order to initialize the LiteRT model with the correct output dimensions.

```python
checkpoint = torch.load(WEIGHTS_PATH, map_location='cpu')

# In case the checkpoint is a dict with a 'state_dict' key
state_dict = (
    checkpoint['state_dict'] 
    if isinstance(checkpoint, dict) and 'state_dict' in checkpoint 
    else checkpoint
)

# Determine the number of classes from the last tensor in the state dict 
last_tensor = state_dict[list(state_dict.keys())[-1]]

num_classes = (
    last_tensor.shape[0] 
    if last_tensor.ndim == 1        # bias vector case
    else min(last_tensor.shape)     # weight matrix case
)

model = mobilenet_v2(num_classes=num_classes)
model.load_state_dict(state_dict, strict=True)
model.eval()

print(model)
```

The example above assumes that the model being loaded is a `MobileNetV2` architecture, but you can replace it with any other architecture.

### 2) Convert PyTorch -> LiteRT

Defining some sample inputs to trace the model and later convert it to LiteRT format with `litert_torch` and finally exporting the generated `.tflite` file to the `artifacts` directory.

```python
sample_inputs = (torch.randn(1, 3, 224, 224),) # Must be a tuple

edge_model = litert_torch.convert(model, sample_inputs)
edge_model.export(str(TFLITE_PATH))
```

### 3) Final check

Just checking that the file was generated and inspecting its size.

```python
print('TFLite path:', TFLITE_PATH)
print('TFLite size (bytes):', TFLITE_PATH.stat().st_size)

interpreter = litert_interpreter.Interpreter(model_path=str(TFLITE_PATH))
interpreter.allocate_tensors()

input_details = interpreter.get_input_details()
output_details = interpreter.get_output_details()

print("Input details:", input_details)
print("Output details:", output_details)
```

---

## The ONNX Version (Deprecated)

This tutorial shows how to convert a PyTorch model into LiteRT format using ONNX as an intermediate format. It's important to note that even though both of this methods work, the `litert_torch` method is the current recommended approach, since this one uses deprecated dependencies and could lead to compatibility issues in the future.

The conversion process involves three main steps:

1. PyTorch model -> ONNX
2. ONNX -> TensorFlow SavedModel
3. SavedModel -> TFLite (`.tflite`)

### Setup

Make sure you have the following dependencies installed in your Python environment, again it is recommended to use a separate virtual environment for this notebook compared to the one used to install the dependencies of `requirements.txt` since some of these have specific version requirements that may conflict with the ones found there.

```python
torch>=2.5.1
torchvision==0.20.1
onnx==1.15.0
onnx-tf==1.10.0
tensorflow==2.15.1
tensorflow-probability==0.23.0
```

You can save these in a `onnx_conversion.txt` file and install them with.

```bash
pip install -r onnx_conversion.txt
```

Run to check that the dependencies are correctly installed.

```python
from pathlib import Path

import torch

from torchvision.models import mobilenet_v2
import tensorflow as tf
import onnx
from onnx_tf.backend import prepare
```

```python
ARTIFACTS_DIR = Path('artifacts')
ARTIFACTS_DIR.mkdir(parents=True, exist_ok=True)

ONNX_PATH = ARTIFACTS_DIR / 'model.onnx'
SAVEDMODEL_DIR = ARTIFACTS_DIR / 'saved_model'
TFLITE_PATH = ARTIFACTS_DIR / 'model.tflite'

WEIGHTS_PATH = ARTIFACTS_DIR / 'mobilenet_v2_best_model.pth'
TFLITE_PATH = ARTIFACTS_DIR / 'mobilenet_v2_litert.tflite'

print('Artifacts dir:', ARTIFACTS_DIR)
```

### 1) Load PyTorch model

Here we load the PyTorch model and extract the number of classes from the final layer, in order to initialize the ONNX model with the correct output dimensions.

```python
checkpoint = torch.load(WEIGHTS_PATH, map_location="cpu")

# In case the checkpoint is a dict with a 'state_dict' key
state_dict = (
    checkpoint['state_dict'] 
    if isinstance(checkpoint, dict) and 'state_dict' in checkpoint 
    else checkpoint
)

# Determine the number of classes from the last tensor in the state dict 
last_tensor = state_dict[list(state_dict.keys())[-1]]

num_classes = (
    last_tensor.shape[0] 
    if last_tensor.ndim == 1        # bias vector case
    else min(last_tensor.shape)     # weight matrix case
)

model = mobilenet_v2(num_classes=num_classes)
model.load_state_dict(state_dict, strict=True)
model.eval()

print(model)
```

### 2) Export PyTorch -> ONNX

Here we define some sample inputs to trace the model and then export it to ONNX format. The parameters used in `torch.onnx.export` are set to be compatible with ONNX Runtime and TensorFlow.

```python
sample_inputs = torch.randn(1, 3, 224, 224)

torch.onnx.export(
    model,
    sample_inputs,
    str(ONNX_PATH),
    export_params=True,
    opset_version=17,
    do_constant_folding=True,
    input_names=["input"],
    output_names=["output"],
    dynamic_axes={"input": {0: "batch"}, "output": {0: "batch"}},
    dynamo=False,
)

print("ONNX exported to:", ONNX_PATH)
```

### 3) Convert ONNX -> TensorFlow SavedModel

This step uses `onnx-tf` to convert the ONNX model into a TensorFlow SavedModel, which is like a directory containing the model architecture and weights in a format that can be easily converted to TFLite.

```python
onnx_model = onnx.load(str(ONNX_PATH))
tf_rep = prepare(onnx_model)
tf_rep.export_graph(str(SAVEDMODEL_DIR))

print("SavedModel exported to:", SAVEDMODEL_DIR)
```

### 4) Convert SavedModel -> LiteRT

Finally we use TensorFlow's TFLiteConverter to convert the SavedModel into a `.tflite` file.

```python
converter = tf.lite.TFLiteConverter.from_saved_model(str(SAVEDMODEL_DIR))

tflite_model = converter.convert()
TFLITE_PATH.write_bytes(tflite_model)
```

### 5) Final check

Just checking that the file was generated, as well as loading it with the TFLite interpreter to check that it's valid.

```python
print('TFLite path:', TFLITE_PATH)
print('TFLite size (bytes):', TFLITE_PATH.stat().st_size)

interpreter = tf.lite.Interpreter(model_path=str(TFLITE_PATH))
interpreter.allocate_tensors()

input_details = interpreter.get_input_details()
output_details = interpreter.get_output_details()

print("Input details:", input_details)
print("Output details:", output_details)
```
