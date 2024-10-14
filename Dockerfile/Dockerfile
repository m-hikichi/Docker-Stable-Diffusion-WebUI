FROM python:3.10
RUN apt-get update && apt-get install -y ffmpeg libsm6 libxext6

# download Base-Model
# After manually downloading the models, place them in the models/checkpoint/Pony directory

# download VAE-approx for sdxl
RUN mkdir -p /tmp/VAE-approx
# https://github.com/AUTOMATIC1111/stable-diffusion-webui/releases/download/v1.0.0-pre/vaeapprox-sdxl.pt : stable-diffusion-webui/modules/sd_vae_approx.py
RUN wget -P /tmp/VAE-approx https://github.com/AUTOMATIC1111/stable-diffusion-webui/releases/download/v1.0.0-pre/vaeapprox-sdxl.pt

# install packages
RUN pip install --upgrade pip
COPY Dockerfile/requirements.txt .
RUN pip install -r requirements.txt

# clone stable-diffusion-webui
RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b v1.10.0
COPY models/checkpoint/Pony/ebara_pony/ebaraPony_ebaraPonyV3.safetensors /stable-diffusion-webui/models/Stable-diffusion/ebara_pony_v3.safetensors
# RUN mv /tmp/VAE/*.safetensors /stable-diffusion-webui/models/VAE
RUN mv /tmp/VAE-approx/vaeapprox-sdxl.pt /stable-diffusion-webui/models/VAE-approx

COPY Dockerfile/download_model.py .
RUN python download_model.py
WORKDIR /stable-diffusion-webui

# --skip-torch-cuda-test, --listen, --xformers : stable-diffusion-webui/modules/cmd_args.py
# --exit : stable-diffusion-webui/modules/launch_utils.py
RUN python launch.py --skip-torch-cuda-test --listen --xformers --exit
