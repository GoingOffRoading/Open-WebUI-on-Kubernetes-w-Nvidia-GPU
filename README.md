# ComfyUI-on-Kubernetes-w-Nvidia-GPU

![Open WebUI](https://github.com/GoingOffRoading/Open-WebUI-on-Kubernetes-w-Nvidia-GPU/blob/main/OpenWebUI.png)

# Abstraction

I'm tinkering with GenAI in my homelab cluster and wasn't finding a lot of examples or documentation related to deploying this stuff to Kubernetes.  I've stood up this repo as a resource incase you find yourself in the same situation, and want to yank some of the learning curve out of GenAI Kubernetes deployments.

# Open WebUI Docker Resources

* [Open WebUI Getting Started](https://docs.openwebui.com/getting-started/)
* Open WebUI [Image Generation](https://docs.openwebui.com/tutorials/features/images/)
* Open WebUI on [Github](https://github.com/open-webui/open-webui)

# Deployment Steps

1. Ensure that you have the [Nvidia drivers installed on the client](https://ubuntu.com/server/docs/nvidia-drivers-installation) and [Nivida Kuberentes plugin installed and enabled](https://github.com/NVIDIA/k8s-device-plugin).
2. Download [Open-WebUI.yml](https://github.com/GoingOffRoading/Open-WebUI-on-Kubernetes-w-Nvidia-GPU/blob/main/Open-WebUI.yml) from this repo.
3. Make changes to the deployment... Most importantly the local directory that Ollama will persist it's volume in, and the nodeName.
4. Assuming you have kubectl installed and configured on this machine, run: `kubectl apply -f comfyui.yml`.
5. Enjoy!  The Open WebUI...  UI...  Is avaliable at the IP address of the nodeName machine, and the port of `32126`
6. Log into the UI and add Ollama: Go to Admin Settings, Click Connections, then add the Ollama API (IP:port)
7. From the same UI, [Follow these steps](https://docs.openwebui.com/tutorials/features/images/#step-1-configure-open-webui-settings) to add ComfyUI for image generation
8. Done!


# Common Questions

* How do I use the image generation?

    Ask Ollama/OpenWeb UI to make a text image prompt, like:

    `Write me an image prompt for a battlefield from the video game halo where three spartans are fighting the covenant on a snowy plain`

    Once that prompt returns, click the little image button.  Depending on your ComfyUI settings, it make take 30-60+ seconds for your image to be returned.

* Can you break out the steps for adding ComfyUI?  

    Yes, if needed

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