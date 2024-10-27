# ComfyUI-on-Kubernetes-w-Nvidia-GPU

![ComfyUI](https://github.com/GoingOffRoading/ComfyUI-on-Kubernetes-w-Nvidia-GPU/blob/main/comfyui.webp)

# Abstraction

I'm tinkering with GenAI in my homelab cluster and wasn't finding a lot of examples or documentation related to deploying this stuff to Kubernetes.  I've stood up this repo as a resource incase you find yourself in the same situation, and want to yank some of the learning curve out of GenAI Kubernetes deployments.

# ComfyUI Docker Resources

There is not an official ComfyUI on Docker from the ComfyUI team that I am aware of, so I had to lean on the work done by [YanWenKun](https://github.com/YanWenKun).


* yanwk/comfyui-boot:cu121 on [Docker Hub](https://hub.docker.com/r/yanwk/comfyui-boot)
* ComfyUI-Docker on [Github](https://github.com/YanWenKun/ComfyUI-Docker)

# Deployment Steps

1. Ensure that you have the [Nvidia drivers installed on the client](https://ubuntu.com/server/docs/nvidia-drivers-installation) and [Nivida Kuberentes plugin installed and enabled](https://github.com/NVIDIA/k8s-device-plugin).
2. Download [ComfyUI.yml](https://github.com/GoingOffRoading/ComfyUI-on-Kubernetes-w-Nvidia-GPU/blob/main/ComfyUI.yml) from this repo.
3. Make changes to the deployment... Most importantly the local directory that Ollama will persist it's volume in, and the nodeName.
4. Assuming you have kubectl installed and configured on this machine, run: `kubectl apply -f comfyui.yml`.
5. Enjoy!  The ComfyUI...  UI...  Is avaliable at the IP address of the nodeName machine, and the port of `32127`

# What is the Configuration for Open WebUI?

These are the steps that I replicated from this [YouTuve video](https://www.youtube.com/watch?v=t68_mYLnSG4):

* Click the gear wheel on the right, and enable `Dev Mode: Enable dev mode options (API save, etc.)`
* Click `Save (API Format)` and hold onto this file for later.  The rest of the steps will be in the Open WebUI repo.

# Common Questions

* Why not resolve any intermiten DNS issues in the cluster instead of calling for `dnsPolicy: "None"`?  Where's the PV/PVC?  Why use `nodeName' instead of setting up affinities?

    All great questions, of which I didn't have time to setup originally.  Please feel free to make your own tweaks, or open up a branch.

* What Nvidia drivers did you install?

    From the link in step 1, I used `sudo ubuntu-drivers install` and let Ubuntu sort it out.  I had a buggy time trying to get the `-server` and `-server -open` drivers to work, but the regular desktop driver worked great.

* What GPU was this tested with?

    PNY Nvidia RTX2000

# Future 

- [ ] Setup a PV/PVC
- [ ] Setup node affinities
- [ ] Resouce limits?