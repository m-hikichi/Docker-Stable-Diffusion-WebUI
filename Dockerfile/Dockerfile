FROM python:3.10

RUN wget -P /tmp/Stable-diffusion https://huggingface.co/WarriorMama777/OrangeMixs/resolve/main/Models/AbyssOrangeMix3/AOM3A1_orangemixs.safetensors
RUN wget -P /tmp/VAE https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.safetensors

RUN pip install --upgrade pip

# install PyTorch 2.0 for CUDA 11.7
# https://pytorch.org/get-started/pytorch-2.0/
RUN pip3 install numpy --pre torch torchvision torchaudio --force-reinstall --index-url https://download.pytorch.org/whl/nightly/cu117

COPY Dockerfile/requirements.txt .
RUN pip install -r requirements.txt

RUN apt-get update && apt-get install ffmpeg libsm6 libxext6  -y

RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b v1.3.2

RUN mv /tmp/Stable-diffusion/*.safetensors /stable-diffusion-webui/models/Stable-diffusion
RUN mv /tmp/VAE/*.safetensors /stable-diffusion-webui/models/VAE

WORKDIR stable-diffusion-webui
RUN python launch.py --skip-torch-cuda-test --exit
