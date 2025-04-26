# Local AI: Ollama + Open WebUI with GPU Support

This guide helps you set up [Ollama](https://ollama.com) with [Open WebUI](https://github.com/open-webui/open-webui) on a Linux system using Docker, with GPU acceleration (NVIDIA).
This version intentionally binds to localhost to keep setup private and limit access strictly to your machine.

---

## ✅ Prerequisites

- Ubuntu (native or WSL2)
- Docker & Docker Compose installed
- NVIDIA GPU
- NVIDIA Container Toolkit (`nvidia-docker2`)

---

## 🧰 Setup Instructions

### 1. Install Docker & Docker Compose

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker $USER
```

> Reboot or log out/log back in after running `usermod`.

---

### 2. Install NVIDIA Container Toolkit

Follow this guide: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/index.html

---

### 3. Verify GPU Access in Docker

```bash
docker run --rm --gpus all nvidia/cuda:12.2.0-base-ubuntu20.04 nvidia-smi
```

> You should see your GPU info.

---

### 4. Start the Containers

```bash
docker compose up -d
```

Check if containers are running:

```bash
docker ps
```

---

## 📥 Download and Run Models

Enter the `ollama` container:

```bash
docker exec -it local_ai_ollama_1 bash
```

Pull a model:

```bash
ollama pull gemma3
```

Run it:

```bash
ollama run gemma3
```

> You can find more models here: https://ollama.com/library

---

## 🌐 Access Web UI

Open in your browser:

## http://localhost:3000

## 🧹 Clean Up

Stop and remove containers:

```bash
docker compose down
```

Remove pulled models:

```bash
ollama list
ollama rm <model-name>
```

---
