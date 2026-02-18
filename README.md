# MODULAR BLENDER COLAB RENDERER 🚀

A high-performance, robust Google Colab notebook designed to render Blender projects using cloud GPUs. This tool automates the entire pipeline: from mounting Google Drive and environment setup to frame rendering and automatic FFmpeg video encoding.

<br>

---

## ✨ Key Features

* **Smart Render Loop**: Supports complex frame ranges and sequences (e.g., `1-10, 20, 35-55`).
* **Format Agnostic**: Automatically detects and moves whatever format Blender outputs (`.png`, `.exr`, `.jpg`).
* **Linear EXR Support**: Specialized FFmpeg handling for `.exr` files, applying gamma correction so preview videos look correct.
* **Auto-Video Encoding**: Interactive FFmpeg integration to stitch frames into an `.mp4` at your custom FPS.
* **Robust Error Handling**: Specific diagnostics for Drive mounting failures, missing engines, or empty project folders.
* **Optimized VRAM Usage**: Provides a choice between **OptiX** (fastest for RTX) and **CUDA** (maximum stability for heavy scenes).
* **Local Processing**: Automatically copies `.blend` files to local storage to bypass Google Drive network latency.

---
<br>

---

## 📂 Directory Structure

To use this notebook, organize your Google Drive as follows:

```text
My Drive/
└── blender/
    ├── blender_tars/    <-- Place your Blender Linux (.tar.xz) files here
    ├── blend_files/     <-- Place your .blend projects here
    └── outputs/         <-- Rendered frames and videos will appear here
```
> **Note:** The script will automatically create these directories on the first run if they do not exist.

---
<br>

---

## 🚀 Getting Started

To begin rendering with the Modular Blender Renderer, follow these steps:

1.  **Upload**: Upload the `ModularBlenderRenderer.ipynb` file to your **Google Drive**.
2.  **Open**: Open the file using **Google Colab**.
3.  **Enable GPU**: 
    * Navigate to `Runtime` > `Change runtime type`.
    * Select a **Hardware Accelerator** (T4, L4, or A100).
4.  **Run**: Execute the cells and follow the **interactive prompts** to:
    * Select your Blender version.
    * Upload/link your project file.
    * Configure your render settings.

> **Note:** Using an A100 or L4 GPU will significantly decrease render times for complex scenes compared to the standard T4.

---
<br>

---

## 🛠️ Render Settings & Defaults

| Setting | Default | Description |
| :--- | :--- | :--- |
| **Engine** | Cycles | Choose between **Cycles** (Ray-traced quality) or **EEVEE** (Real-time speed). |
| **Resolution %** | 100% | Scale output dimensions (e.g., 50% for 4x faster previews). |
| **Device** | CUDA | **CUDA** for high stability; **OptiX** for RTX hardware acceleration. |
| **FPS** | 24 | The frame rate for the generated .mp4 preview video. |

---
<br>

---

## ❓ Troubleshooting

### Scene Crashing or "Out of Memory"
If your scene is extremely heavy (like the Lone Monk demo), choose **CUDA** instead of **OptiX**. 

* **CUDA** handles VRAM spikes and system RAM swapping more gracefully.
* **OptiX** has higher memory overhead for its acceleration structures, which can lead to crashes on heavy scenes.

### Dark EXR Video Previews
The script automatically applies a `gamma=2.2` filter when it detects `.exr` frames during the video encoding stage. This ensures the resulting `.mp4` matches the standard **sRGB color space** instead of looking "washed out" or dark.

### Drive Mounting Issues
If the drive fails to mount:
1. Ensure **third-party cookies** are enabled for `googleusercontent.com` in your browser settings.
2. Use the **folder icon** in the Colab sidebar to mount manually.

---
<br>

---

## 📝 License
This project is open-source and available under the **MIT License**.

---
