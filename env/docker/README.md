# prepare the model
```
dianfan@zyszhome-ubuntu-dev:~/devroot/src/stable-diffusion-webui-devkit$ tree models/
models/
├── Codeformer
├── deepbooru
│   └── Put your deepbooru release project folder here.txt
├── ESRGAN
├── GFPGAN
├── hypernetworks
│   ├── aini.pt
│   ├── anime_2.pt
│   ├── anime_3.pt
│   ├── anime.pt
│   ├── furry_2.pt
│   ├── furry_3.pt
│   ├── furry_kemono.pt
│   ├── furry_protogen.pt
│   ├── furry.pt
│   ├── furry_scalie.pt
│   ├── furry_transformation.pt
│   └── pony.pt
├── LDSR
├── Stable-diffusion
│   ├── model.ckpt
│   ├── model.vae.pt
│   └── Put Stable Diffusion checkpoints here.txt
├── SwinIR
└── VAE
    ├── animevae.pt
    └── Put VAE here.txt
```

# build the docker defvbox
```
docker build -t ai-drawing-devbox .
```

# run the docker image
```
docker run --rm -it -v /home/dianfan/devroot/src/:/mnt/devroot/ -v /mnt/DataExt/devroot/:/mnt/DataExt/devroot/ -w /mnt/devroot/stable-diffusion-webui-devkit/ -v ~/.ssh:/root/.ssh -p 7860:7860 --cpus=16 --gpus all --pids-limit=-1 --memory=84g --shm-size=84g --privileged --runtime nvidia -e NVIDIA_DRIVER_CAPABILITIES=video,compute,utility --name ai-drawing-container ai-drawing-devbox /bin/bash
```

# launch the app
```
./webui.sh -f --listen
```

