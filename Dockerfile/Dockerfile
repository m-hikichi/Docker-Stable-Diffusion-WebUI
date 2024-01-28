FROM python:3.10
RUN apt-get update && apt-get install -y ffmpeg libsm6 libxext6

# download Base-Model
RUN mkdir -p /tmp/Stable-diffusion
RUN wget -O /tmp/Stable-diffusion/AOM3A1.safetensors https://huggingface.co/WarriorMama777/OrangeMixs/resolve/main/Models/AbyssOrangeMix3/AOM3A1_orangemixs.safetensors

# download VAE
RUN mkdir -p /tmp/VAE
RUN wget -P /tmp/VAE https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.safetensors

# install packages
RUN pip install --upgrade pip
COPY requirements.txt .
RUN pip install -r requirements.txt

# clone stable-diffusion-webui
RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b v1.7.0
RUN mv /tmp/Stable-diffusion/*.safetensors /stable-diffusion-webui/models/Stable-diffusion
RUN mv /tmp/VAE/*.safetensors /stable-diffusion-webui/models/VAE

COPY download_model.py .
RUN python download_model.py
WORKDIR /stable-diffusion-webui
RUN python launch.py --skip-torch-cuda-test --listen --xformers --exit
