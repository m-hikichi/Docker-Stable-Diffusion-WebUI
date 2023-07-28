FROM python:3.10

# download Base-Model
RUN mkdir -p /tmp/Stable-diffusion
RUN wget -O /tmp/Stable-diffusion/AOM3A1.safetensors https://huggingface.co/WarriorMama777/OrangeMixs/resolve/main/Models/AbyssOrangeMix3/AOM3A1_orangemixs.safetensors

# download VAE
RUN mkdir -p /tmp/VAE
RUN wget -P /tmp/VAE https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.safetensors

# download ControlNet-Model
RUN mkdir -p /tmp/ControlNet
RUN wget -P /tmp/ControlNet https://huggingface.co/lllyasviel/ControlNet-v1-1/resolve/main/control_v11p_sd15_inpaint.pth
RUN wget -P /tmp/ControlNet https://huggingface.co/lllyasviel/ControlNet-v1-1/resolve/main/control_v11p_sd15_lineart.pth

# install packages
RUN pip install --upgrade pip
COPY Dockerfile/requirements.txt .
RUN pip install -r requirements.txt
RUN apt-get update && apt-get install ffmpeg libsm6 libxext6  -y

# clone stable-diffusion-webui
RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b v1.5.0
RUN mv /tmp/Stable-diffusion/*.safetensors /stable-diffusion-webui/models/Stable-diffusion
RUN mv /tmp/VAE/*.safetensors /stable-diffusion-webui/models/VAE

# clone sd-webui-controlnet
WORKDIR /stable-diffusion-webui/extensions
RUN git clone https://github.com/Mikubill/sd-webui-controlnet.git
RUN mv /tmp/ControlNet/*.pth /stable-diffusion-webui/extensions/sd-webui-controlnet/models

WORKDIR /stable-diffusion-webui
RUN python launch.py --skip-torch-cuda-test --listen --enable-insecure-extension-access --exit
