# Don't use this, it's a WIP

# Docker image for A1111 Stable Diffusion Web UI, Kohya_ss and ComfyUI

Now with SDXL support.

## Installs

* Ubuntu 22.04 LTS
* CUDA 11.8
* Python 3.10.12
* [Automatic1111 Stable Diffusion Web UI](
  https://github.com/AUTOMATIC1111/stable-diffusion-webui.git) 1.6.0
* [Dreambooth extension](
  https://github.com/d8ahazard/sd_dreambooth_extension) 1.0.14
* [Deforum extension](
  https://github.com/deforum-art/sd-webui-deforum)
* [ControlNet extension](
  https://github.com/Mikubill/sd-webui-controlnet) v1.1.410
* [After Detailer extension](
  https://github.com/Bing-su/adetailer) v23.9.2
* [Photopea Webui extension](https://github.com/yankooliveira/sd-webui-photopea-embed)
* [BatchLinks Downloader extension](https://github.com/etherealxx/batchlinks-webui)
* [Inpaint Anything extension](https://github.com/Uminosachi/inpaint-anything)
* [Infinite Image Browsing extension](https://github.com/zanllp/sd-webui-infinite-image-browsing)
* [Locon extension](
  https://github.com/ashleykleynhans/a1111-sd-webui-locon)
* [roop extension](https://github.com/s0md3v/sd-webui-roop) 0.0.2
* [Kohya_ss](https://github.com/bmaltais/kohya_ss) v21.8.10
* [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
* [ComfyUI Manager](https://github.com/ltdrdata/ComfyUI-Manager.git)
* Torch 2.0.1
* xformers 0.0.21
* sd_xl_base_1.0.safetensors
* sd_xl_refiner_1.0.safetensors
* sdxl_vae.safetensors
* inswapper_128.onnx
* [runpodctl](https://github.com/runpod/runpodctl)
* [croc](https://github.com/schollz/croc)
* [rclone](https://rclone.org/)
* [Application Manager](https://github.com/ashleykleynhans/app-manager)

## Available on RunPod

This image is designed to work on [RunPod](https://runpod.io). It's a slightly modified version of [ashleykleynhan's stable-diffusion-docker](
ttps://github.com/ashleykleynhans/stable-diffusion-docker), which can be run directly from [Runpod here](https://runpod.io/gsc?template=ya6013lj5a&ref=2xxro4sy)

##Build the Docker image in Windows

Since the Stable Diffusion models are pretty large, you will need at least
8GB of system memory (not GPU VRAM) to build this image.

The image **CAN** be built on a `t3a.large` AWS EC2 instance
which has 2 x vCPU and 8GB of system memory.  It **CANNOT** be built on
any instances with less memory, eg. `t3a.medium`.

Create a dummy folder on your machine so that you don't clutter things up. Anywhere you want.

```bash
# Clone the repo into this folder
cd Users/Your/DummyFolder
git clone https://github.com/ylfrs/stable-diffusion-docker-Improved.git
```
The repo link should be your modified repository. 

# Download the models

DON'T use wget to download the models into the folder. It's slow, and as I had to find out for myself, the syntax in Windows is different from Linux. Just don't do it.

Copy/paste the models from your local webui install if you already have them, or download directly to the folder if you don't want them on your local machine. Make sure the model names exactly match the way they are referenced in your git repository code. If not, they will not load.

# Build the image

Now that you've got all your goodies in one basket, it's time to build the image:

Make sure Docker Desktop is running, and use the following command

```bash
# Build and tag the image
docker build stable-diffusion-docker-Improved -t username/image-name:1.0.0
```
the tag (everything after "-t" in the line above) is completely up to you, name it whatever you want. 

# Open Docker Desktop

Make sure to have Docker Desktop running, and make sure it's not running on resource saver mode. 

# Push the image to Docker Hub

```bash
docker push username/image-name:1.0.0
```
Resist the temptation to scroll inside the command line after executing this command, as this will cause Docker to print status bars all over, making it difficult to check on the progress of items. Depending on how large your image is, this process could take hours. It failed the first time I tried it. If it fails, delete the Docker repository and push the image again. 

## Running Locally

### Install Nvidia CUDA Driver

- [Linux](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)
- [Windows](https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html)

### Start the Docker container

```bash
docker run -d \
  --gpus all \
  -v /workspace \
  -p 3000:3001 \
  -p 3010:3011 \
  -p 3020:3021 \
  -p 6006:6066 \
  -p 8888:8888 \
  -e JUPYTER_PASSWORD=Jup1t3R! \
  -e ENABLE_TENSORBOARD=1 \
  ashleykza/stable-diffusion-webui:3.1.0
```

You can obviously substitute the image name and tag with your own.

## Acknowledgements

1. [RunPod](https://runpod.io?ref=2xxro4sy) for providing most
   of the [container](https://github.com/runpod/containers) code.
2. Dr. Furkan Gözükara for his amazing
   [YouTube videos](https://www.youtube.com/@SECourses/videos]).
3. [Bernard Maltais](https://github.com/bmaltais) (core developer of Kohya_ss)
   for assisting with optimizing the Docker image.


