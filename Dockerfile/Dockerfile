FROM python:3.10
RUN apt-get update && apt-get install -y ffmpeg libsm6 libxext6

# download Base-Model
# After manually downloading the models, place them in the models/checkpoint/Pony directory

# download VAE
RUN mkdir -p /tmp/VAE
RUN wget -P /tmp/VAE https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.safetensors

# install packages
RUN pip install --upgrade pip
COPY Dockerfile/requirements.txt .
RUN pip install -r requirements.txt

# clone stable-diffusion-webui
RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b v1.10.0
COPY models/checkpoint/SD1.5/OrangeMixs/VividOrangeMix.safetensors /stable-diffusion-webui/models/Stable-diffusion/VividOrangeMix.safetensors
RUN mv /tmp/VAE/*.safetensors /stable-diffusion-webui/models/VAE

COPY Dockerfile/download_model.py .
RUN python download_model.py
WORKDIR /stable-diffusion-webui

# --skip-torch-cuda-test, --listen, --xformers : stable-diffusion-webui/modules/cmd_args.py
# --exit : stable-diffusion-webui/modules/launch_utils.py
RUN python launch.py --skip-torch-cuda-test --listen --xformers --exit
