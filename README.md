The repository contains Jupyter notbooks for using in vast.ai GPU container instance (may work in google colab too) to start a ComfyUI environment. Some example workflows are included as well.

# Jupyter notebook for configuring google colab
## ComfyUI.ipynb
Create a GPU VM container in vast.ai. I use this containter instance template https://cloud.vast.ai/?ref_id=198451&creator_id=198451&name=NVIDIA%20CUDA%2012.1.1%20(Ubuntu).

I usually ise disk size 75 GB and rent RTX 3090 GPUs and create an Instance.

Once the instance is started and connected in instances section click 'Connect directly via Jupyter' button on bottom right. Ignore privacy error in browser and proceed. Once Jupyter file manger is loaded upload ComfyUI.ipynb 
(If Jupyter is not loading delete the instance and create another instance with another RTX 3090 GPU from another location.) Click on uploaded ComfyUI.ipynb. The notebook will open in a new tab.

Click the cell under title 'Install required apt packages' and click 'run' button (▶) to install packages required and to set python version to 3.11.

Once the cell runs completly and shows '-= Done. =-' in log window below the cell run next cell under 'Environment Setup'. This will take time. In this cell we install necessary python modules. ComfyUI and ComfyUI manager.

Once completed we can install some models for ComfyUI using the cell under 'Download models'. Replace '<Enter your Huggingface token here>' with your huggingface token. (Refer https://huggingface.co/docs/hub/en/security-tokens)

Following models are set to download by default. You can comment unwanted models before running the cell. It will take sometime to download the models from huggingface.

* stable-diffusion-v1-5
* flux1-schnell-Q6_K
* FLUX text encoder clip_l.safetensors
* google t5xxl_fp8_e4m3fn encoder
* FLUX ae.safetensors VAE
* InstantX/FLUX.1-dev-Controlnet-Union diffusion_pytorch_model Controlnet
* Kim2091/ClearRealityV1 4x-ClearRealityV1 upscale model
* guozinan pulid_flux_v0.9.0 pulid model
* antelopev2 insightface model
* alimama-creative/FLUX.1-Turbo-Alpha diffusion_pytorch_model LORA
* Bingsu/adetailer face_yolov8n_v2 ultralytics model

Once the models are downloaded we need to access the ComfyUI web UI by either tunneling it through Rathole (https://github.com/rapiz1/rathole) or cloudflare tunnel.

For Rathole tunnel you need a rathole running in server mode in a VPS. Replace '<Enter your rathole server IP>' with your Rathole server IP adderss and configure rathole server to tunnel 54321 (The port in which our ComfyUI web UI runs). 
Then run 'Install rathole and configure' and 'Start Rathole tunnel and ComfyUI' cells and access the comfyUI web UI using <Your rathole server IP>:54321. Please refer https://github.com/rapiz1/rathole for details about rathole configuration and usage.

If you want to use cloudflare tunnel skip 'Install rathole and configure' and 'Start Rathole tunnel and ComfyUI' and go to 'Install cloudflare'. Run that cell and once done Run 'Start cloudflare tunnel and ComfyUI'. 
Check for the URL after 'This is the URL to access ComfyUI:' under the log window of 'Start cloudflare tunnel and ComfyUI' and click it. Now you can access the ComfyUI web UI from our instance.

## Sample ComfyUI workflows.
### FLUX LORA.json 
This is a simple flow to generate images using FLUX model and a LORA. Import the flow using ComfyUI and install missing custom nodes and restart ComfyUI.

### COMFYUI_CHARACTER.json 
This is a complex workflow based on https://youtu.be/Uls_jXy9RuU?si=cy46qV5O1bleD8Dy
You may need to upload Pose_sheet_v02.png and sample.webp to relevant nodes in this workflow.
