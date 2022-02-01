# GPU support with k3d

[k3d][] says it's 'a lightweight wrapper to run k3s (Rancher Lab’s minimal 
Kubernetes distribution) in docker'. Well yes, that's what it does, and it 
does it great. We use [k3d][] for daily development. Thus, you can assume 
that Os4ML runs stably on [k3d][].

So, what about GPU support? [k3d][] describes it in their documentation
[here](https://k3d.io/v5.2.2/usage/advanced/cuda/).If you have 
problems building the Docker image, remember to install the 
`nvidia-container-toolkit` in addition to the `nvidia-container-runtime`.

[k3d]: https://k3d.io

