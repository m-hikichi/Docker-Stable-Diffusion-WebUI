FROM python:3.10

RUN pip install --upgrade pip

COPY Dockerfile/requirements.txt .
RUN pip install -r requirements.txt

RUN apt-get update && apt-get install ffmpeg libsm6 libxext6  -y

RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b v1.2.0

COPY models/stable-diffusion/*.safetensors /stable-diffusion-webui/models/Stable-diffusion
COPY models/vae/*.safetensors /stable-diffusion-webui/models/VAE

WORKDIR stable-diffusion-webui
RUN python launch.py --skip-torch-cuda-test --skip-version-check --listen --enable-insecure-extension-access --exit
