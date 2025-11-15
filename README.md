# ABOV3 Pauline TTS Server: OpenAI-Compatible API with Web UI, Large Text Handling & Built-in Voices

**Self-host high-quality text-to-speech with voice cloning and audiobook generation powered by the [Chatterbox TTS model](https://github.com/resemble-ai/chatterbox) by Resemble AI.**

> 🎙️ **ABOV3 Pauline** provides professional-quality voice synthesis with an intuitive interface, intelligent text processing, and production-ready deployment options.

This server builds upon the [Chatterbox TTS model by Resemble AI](https://github.com/resemble-ai/chatterbox) with enhanced features for production deployment. Runs accelerated on NVIDIA (CUDA), AMD (ROCm), and Apple Silicon (MPS) GPUs, with automatic fallback to CPU.

[![Project Link](https://img.shields.io/badge/GitHub-ABOV3AI/abov3--pauline--tts-blue?style=for-the-badge&logo=github)](https://github.com/ABOV3AI/abov3-pauline-tts)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![Python Version](https://img.shields.io/badge/Python-3.10+-blue.svg?style=for-the-badge)](https://www.python.org/downloads/)
[![Framework](https://img.shields.io/badge/Framework-FastAPI-green.svg?style=for-the-badge)](https://fastapi.tiangolo.com/)
[![Model Source](https://img.shields.io/badge/Model-ResembleAI/chatterbox-orange.svg?style=for-the-badge)](https://github.com/resemble-ai/chatterbox)
[![Docker](https://img.shields.io/badge/Docker-Supported-blue.svg?style=for-the-badge)](https://www.docker.com/)
[![CUDA Compatible](https://img.shields.io/badge/NVIDIA_CUDA-Compatible-76B900?style=for-the-badge&logo=nvidia&logoColor=white)](https://developer.nvidia.com/cuda-zone)
[![ROCm Compatible](https://img.shields.io/badge/AMD_ROCm-Compatible-ED1C24?style=for-the-badge&logo=amd&logoColor=white)](https://rocm.docs.amd.com/)
[![MPS Compatible](https://img.shields.io/badge/Apple_MPS-Compatible-000000?style=for-the-badge&logo=apple&logoColor=white)](https://developer.apple.com/metal/)
[![API](https://img.shields.io/badge/OpenAI_Compatible_API-Ready-000000?style=for-the-badge&logo=openai&logoColor=white)](https://platform.openai.com/docs/api-reference)

---

## 🗣️ Overview: Production-Ready TTS

ABOV3 Pauline TTS Server provides enterprise-grade text-to-speech capabilities with voice cloning, large text processing, and audiobook generation. Built on the powerful Chatterbox TTS model, it offers:

*   A **modern Web UI** for easy experimentation, voice management, and generation parameter tuning
*   **Multi-Platform Acceleration:** Full support for **NVIDIA (CUDA)**, **AMD (ROCm)**, and **Apple Silicon (MPS)** GPUs with automatic **CPU** fallback
*   **Large Text Handling:** Intelligently splits long texts into manageable chunks based on sentence structure and seamlessly concatenates audio
*   **📚 Audiobook Generation:** Create complete audiobooks from full-length texts with consistent voice quality
*   **28 Predefined Voices:** Curated, production-ready synthetic voices for immediate use
*   **Voice Cloning:** Generate speech using uploaded reference audio files
*   **Optimized Audio Quality:** Pre-configured with professional settings for calm, clear delivery (temperature: 0.6, exaggeration: 0.8, cfg_weight: 0.7)
*   **Docker Support:** One-command deployment with GPU acceleration

## ✨ Key Features

**🚀 Core Functionality:**

*   **Large Text Processing (Chunking):**
    *   Automatically handles long plain text by splitting into sentence-based chunks
    *   Ideal for **audiobook generation** - paste entire books and get professional narration
    *   Configurable chunk size and split toggle in UI
*   **28 Production-Ready Voices:**
    *   Includes Emily, Gabriel, Olivia, and 25 more curated voices
    *   Categorized by style (professional, friendly, authoritative, etc.)
    *   Stored in `./voices` directory, selectable via UI dropdown
*   **Voice Cloning:**
    *   Clone any voice using reference audio (`.wav` or `.mp3`)
    *   Upload reference files through Web UI
*   **Optimized Generation:**
    *   Pre-configured for calm, professional delivery
    *   Adjustable temperature, exaggeration, CFG weight, seed, and speed
    *   Consistent voice output across generations

**🔧 Enhanced Server Features:**

*   **OpenAI-Compatible API:** Drop-in replacement for OpenAI TTS endpoints
*   **Interactive API Docs:** Swagger UI at `/docs`
*   **Health Check Endpoint:** `/api/ui/initial-data` for monitoring
*   **Audio Post-Processing:** Optional silence trimming and artifact removal
*   **Session Persistence:** Remembers UI settings via `config.yaml`
*   **Light/Dark Mode:** Theme toggle with preference saved

**🌐 Web Interface:**

*   Modern, responsive UI with intuitive controls
*   Preset loading from `ui/presets.yaml`
*   Reference/predefined audio upload and management
*   Real-time audio playback with waveform visualization ([WaveSurfer.js](https://wavesurfer.xyz/))
*   Configuration management directly in UI
*   Warning modals for generation quality

## 🔩 System Prerequisites

*   **Operating System:** Windows 10/11 (64-bit) or Linux (Debian/Ubuntu recommended)
*   **Python:** Version 3.10 or later
*   **Git:** For cloning the repository
*   **Internet:** For downloading dependencies and models
*   **(Optional but Recommended for Performance):**
    *   **NVIDIA GPU:** CUDA-compatible (Maxwell or newer)
    *   **AMD GPU:** ROCm-compatible (RX 6000/7000 series)
    *   **Apple Silicon:** M1/M2/M3 with macOS 12.3+

## 🐳 Quick Start with Docker (Recommended)

The fastest way to get started:

```bash
# Clone the repository
git clone https://github.com/ABOV3AI/abov3-pauline-tts.git
cd abov3-pauline-tts

# For NVIDIA GPU:
docker compose up -d

# For AMD ROCm GPU:
docker compose -f docker-compose-rocm.yml up -d

# For CPU only:
docker compose -f docker-compose-cpu.yml up -d
```

Access the Web UI at `http://localhost:8004`

See [Docker Installation](#-docker-installation) section below for detailed setup.

## 💻 Manual Installation

### 1. Clone the Repository
```bash
git clone https://github.com/ABOV3AI/abov3-pauline-tts.git
cd abov3-pauline-tts
```

### 2. Create Virtual Environment

**Windows (PowerShell):**
```powershell
python -m venv venv
.\venv\Scripts\activate
```

**Linux/macOS (Bash):**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

**For CPU:**
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

**For NVIDIA GPU (CUDA):**
```bash
pip install --upgrade pip
pip install -r requirements-nvidia.txt
```

**For AMD GPU (ROCm):**
```bash
pip install --upgrade pip
pip install -r requirements-rocm.txt
```

**For Apple Silicon (MPS):**
```bash
pip install --upgrade pip
pip install torch torchvision torchaudio
pip install --no-deps git+https://github.com/resemble-ai/chatterbox.git
pip install fastapi 'uvicorn[standard]' librosa safetensors soundfile pydub audiotsm praat-parselmouth python-multipart requests aiofiles PyYAML watchdog unidecode inflect tqdm
pip install conformer==0.3.2 diffusers==0.29.0 resemble-perth==1.0.1 transformers==4.46.3
pip install --no-deps s3tokenizer
pip install onnx==1.16.0
```

### 4. Run the Server

```bash
python server.py
```

**First run:** The server will download the Chatterbox model (~2-3 GB). This is automatic and one-time only.

Access the UI at `http://localhost:8004`

## ⚙️ Configuration

All settings are managed through `config.yaml` in the project root:

*   **server:** `host`, `port`, logging
*   **model:** `repo_id` (ResembleAI/chatterbox)
*   **tts_engine:** `device` (auto/cuda/mps/cpu), voice paths
*   **generation_defaults:** Optimized settings (temperature: 0.6, exaggeration: 0.8, cfg_weight: 0.7)
*   **ui:** Title, language select, voice dropdown limits

Changes to server/model/engine require restart. Generation defaults apply immediately.

## 💡 Usage

### Web UI

*   **Text Input:** Enter text or paste entire book for audiobook generation
*   **Voice Mode:** Choose from 28 predefined voices or use voice cloning
*   **Parameters:** Adjust temperature, exaggeration, speed, seed
*   **Chunking:** Enable for long texts with adjustable chunk size
*   **Audio Player:** Play generated audio with waveform, download option

### API Endpoints

**Primary TTS Endpoint:**
```bash
POST /tts
{
  "text": "Your text here",
  "voice_mode": "predefined",  # or "clone"
  "predefined_voice_id": "Emily.wav",
  "temperature": 0.6,
  "exaggeration": 0.8,
  "cfg_weight": 0.7,
  "split_text": true,
  "chunk_size": 120
}
```

**OpenAI-Compatible Endpoint:**
```bash
POST /v1/audio/speech
{
  "input": "Your text here",
  "voice": "Emily.wav",
  "response_format": "mp3",
  "speed": 1.0
}
```

See `/docs` for complete API documentation.

## 🐳 Docker Installation

### Prerequisites

*   [Docker](https://docs.docker.com/get-docker/) installed
*   [Docker Compose](https://docs.docker.com/compose/install/) (included with Docker Desktop)
*   **(For GPU):** NVIDIA Container Toolkit or ROCm drivers

### Using Docker Compose

#### NVIDIA GPU:
```bash
docker compose up -d
```

#### AMD ROCm GPU:
```bash
# Add user to required groups (one-time)
sudo usermod -a -G video,render $USER
# Log out and back in

docker compose -f docker-compose-rocm.yml up -d
```

#### CPU Only:
```bash
docker compose -f docker-compose-cpu.yml up -d
```

### Verify GPU Access

**NVIDIA:**
```bash
docker compose exec abov3-pauline-tts nvidia-smi
docker compose exec abov3-pauline-tts python3 -c "import torch; print(f'CUDA: {torch.cuda.is_available()}')"
```

**AMD ROCm:**
```bash
docker compose -f docker-compose-rocm.yml exec abov3-pauline-tts rocm-smi
docker compose -f docker-compose-rocm.yml exec abov3-pauline-tts python3 -c "import torch; print(f'ROCm: {torch.cuda.is_available()}')"
```

### Container Management

```bash
# View logs
docker compose logs -f

# Stop container
docker compose down

# Restart container
docker compose restart abov3-pauline-tts
```

## 🔍 Troubleshooting

*   **CUDA Not Available:** Check `nvidia-smi`, verify NVIDIA drivers and Container Toolkit
*   **VRAM OOM:** Reduce `chunk_size`, close other GPU applications
*   **ROCm GPU Not Detected:** Verify `groups $USER` includes `video` and `render`
*   **Model Download Fails:** Check internet connection, verify `model.repo_id` in config
*   **Port Conflict:** Change `server.port` in `config.yaml` or use `PORT=8005 docker compose up -d`

## 🤝 Contributing

Contributions welcome! Open an issue or submit a Pull Request.

## 📜 License

This project is licensed under the **MIT License**. See [LICENSE](LICENSE) file for details.

## 🙏 Attribution & Acknowledgements

### Original Project

**ABOV3 Pauline TTS** is a fork/rebrand of [Chatterbox TTS Server](https://github.com/devnen/Chatterbox-TTS-Server) by [devnen](https://github.com/devnen).

**Original Project:**
*   Repository: https://github.com/devnen/Chatterbox-TTS-Server
*   Author: devnen
*   License: MIT License

### ABOV3 Modifications

*   Rebranded as ABOV3 Pauline TTS
*   Optimized default configuration for production (calm, professional voice)
*   Enhanced documentation and deployment guides
*   Custom voice presets and examples
*   Docker image published to GitHub Container Registry

### Core Technologies

*   **TTS Model:** [Chatterbox TTS](https://github.com/resemble-ai/chatterbox) by [Resemble AI](https://www.resemble.ai/)
*   **Framework:** [FastAPI](https://fastapi.tiangolo.com/), [Uvicorn](https://www.uvicorn.org/)
*   **ML Libraries:** [PyTorch](https://pytorch.org/), [Hugging Face](https://huggingface.co/)
*   **Audio:** [SoundFile](https://python-soundfile.readthedocs.io/), [WaveSurfer.js](https://wavesurfer.xyz/)
*   **Containerization:** [Docker](https://www.docker.com/), [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-docker)

---

**Developed by [ABOV3AI](https://github.com/ABOV3AI) | Based on Chatterbox TTS Server**
