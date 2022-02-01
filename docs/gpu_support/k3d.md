# GPU support with k3d

[k3d][] says it's 'a lightweight wrapper to run k3s (Rancher Lab’s minimal 
Kubernetes distribution) in docker'. Well yes, they are right, and they are 
great. This is the reason why we use [k3d][] for our daily development work. 
For this reason it can be assumed that Os4ML runs stably on [k3d][].

It's quite nice to equip k3d with gpu support as described 
[here](https://k3d.io/v5.2.2/usage/advanced/cuda/).If you have problems 
building the Docker image, remember to install the 
`nvidia-container-toolkit` in addition to the `nvidia-container-runtime`.

[k3d]: https://k3d.io

