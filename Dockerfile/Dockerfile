FROM python:3.10
RUN apt-get update && apt-get install -y ffmpeg libsm6 libxext6

# download Base-Model
RUN mkdir -p /tmp/Stable-diffusion
RUN wget -O /tmp/Stable-diffusion/Animagine_XL_V3.1.safetensors https://huggingface.co/cagliostrolab/animagine-xl-3.1/resolve/main/animagine-xl-3.1.safetensors

# # download VAE
# RUN mkdir -p /tmp/VAE
# RUN wget -P /tmp/VAE https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.safetensors

# download VAE-approx for sdxl
RUN mkdir -p /tmp/VAE-approx
# https://github.com/AUTOMATIC1111/stable-diffusion-webui/releases/download/v1.0.0-pre/vaeapprox-sdxl.pt : stable-diffusion-webui/modules/sd_vae_approx.py
RUN wget -P /tmp/VAE-approx https://github.com/AUTOMATIC1111/stable-diffusion-webui/releases/download/v1.0.0-pre/vaeapprox-sdxl.pt

# install packages
RUN pip install --upgrade pip
COPY requirements.txt .
RUN pip install -r requirements.txt

# clone stable-diffusion-webui
RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b v1.10.0
RUN mv /tmp/Stable-diffusion/*.safetensors /stable-diffusion-webui/models/Stable-diffusion
# RUN mv /tmp/VAE/*.safetensors /stable-diffusion-webui/models/VAE
RUN mv /tmp/VAE-approx/vaeapprox-sdxl.pt /stable-diffusion-webui/models/VAE-approx

COPY download_model.py .
RUN python download_model.py
WORKDIR /stable-diffusion-webui

# --skip-torch-cuda-test, --listen, --xformers : stable-diffusion-webui/modules/cmd_args.py
# --exit : stable-diffusion-webui/modules/launch_utils.py
RUN python launch.py --skip-torch-cuda-test --listen --xformers --exit
