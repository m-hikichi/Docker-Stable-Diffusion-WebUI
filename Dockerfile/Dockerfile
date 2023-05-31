FROM python:3.10

RUN pip install --upgrade pip

# install PyTorch 2.0 for CUDA 11.7
# https://pytorch.org/get-started/pytorch-2.0/
RUN pip3 install numpy --pre torch torchvision torchaudio --force-reinstall --index-url https://download.pytorch.org/whl/nightly/cu117

COPY Dockerfile/requirements.txt .
RUN pip install -r requirements.txt

RUN apt-get update && apt-get install ffmpeg libsm6 libxext6  -y

RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git -b v1.3.0

COPY models/stable-diffusion/*.safetensors /stable-diffusion-webui/models/Stable-diffusion
COPY models/vae/*.safetensors /stable-diffusion-webui/models/VAE

WORKDIR stable-diffusion-webui
RUN python launch.py --skip-torch-cuda-test --exit
