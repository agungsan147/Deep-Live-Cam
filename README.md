## Installation (Windows)

> **Requirements**
>
> - Windows 10/11 (64-bit)
> - Python 3.11
> - Git
> - FFmpeg
> - Microsoft Visual Studio 2022 Build Tools (Desktop development with C++)
> - NVIDIA GPU (Optional, recommended)

---

### 1. Clone Repository

```bash
git clone --depth 1 https://github.com/hacksider/Deep-Live-Cam.git
cd Deep-Live-Cam
```

---

### 2. Download Models

Download the following models:

- GFPGANv1.4.onnx
- https://github.com/TencentARC/GFPGAN/releases/download/v1.3.4/GFPGANv1.4.pth


- inswapper_128_fp16.onnx
- https://huggingface.co/hacksider/deep-live-cam/resolve/main/inswapper_128_fp16.onnx?download=true

Move both files into the `models` folder.

---

### 3. Create Virtual Environment

```bash
python -m venv venv
```

Activate it:

```bash
venv\Scripts\activate
```

---

### 4. Install Python Dependencies

```bash
pip install -r requirements.txt
```

> **If `insightface` fails to install**
>
> Install **Microsoft Visual Studio 2022 Build Tools** and enable:
>
> - Desktop development with C++
> - MSVC v143 Build Tools
> - Windows 10/11 SDK

After installation, run:

```bash
pip install -r requirements.txt
```

again.

---

# GPU Acceleration (NVIDIA CUDA)

### 1. Install CUDA Toolkit 12.8

Download and install:

https://developer.nvidia.com/cuda-12-8-0-download-archive

Restart Windows after installation.

Verify:

```bash
nvcc --version
```

---

### 2. Install PyTorch (CUDA 12.8)

```bash
pip install -U torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128
```

---

### 3. Install ONNX Runtime GPU

```bash
pip uninstall onnxruntime onnxruntime-gpu
pip install onnxruntime-gpu==1.21.0
```

---

### 4. Verify CUDA

```bash
python -c "import onnxruntime as ort; print(ort.get_available_providers())"
```

Expected output:

```text
['TensorrtExecutionProvider',
 'CUDAExecutionProvider',
 'CPUExecutionProvider']
```

---

### 5. Run

```bash
python run.py --execution-provider cuda
```

If everything is configured correctly, the console should display:

```text
Applied providers: ['CUDAExecutionProvider']
```

---

## CPU Mode

Run normally:

```bash
python run.py
```

---

## Usage

### Image / Video

1. Launch:

```bash
python run.py
```

2. Select a source face.

3. Select a target image or video.

4. Click **Start**.

The processed file will be saved automatically.

---

### Webcam

Launch:

```bash
python run.py --execution-provider cuda
```

1. Select a source face.
2. Click **Live**.
3. Wait until the webcam preview appears.
4. Use OBS or other capture software if you want to stream.

---

## Download All Models

https://huggingface.co/hacksider/deep-live-cam/tree/main
