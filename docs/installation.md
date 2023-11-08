# Installation
Nobody wants complicated installations. We neither. For this reason we 
provided [Terraform] scripts in the past to install fully functional 
[Os4ML] on a [k3d] cluster.

## k3d cluster
[k3d] says it's 'a lightweight wrapper to run k3s (Rancher Lab’s minimal 
Kubernetes distribution) in docker'. Well yes, that's what it does, and it 
does it great. We use [k3d] for daily development. Thus, you can assume 
that Os4ML runs stably on [k3d].

With [k3d] you can do it like this, for example

```sh
git clone https://github.com/WOGRA-AG/terraform-kustomization-os4ml.git
cd terraform-kustomization-os4ml
k3d cluster create --config ./k3d-default.yaml
terraform init
terraform apply -auto-approve
```

This will install [ArgoCD] in the cluster and then ArgoCD will then take care of installing Os4ml on its own.

## GPU Support
For sure, if you want to do machine learning, you want to use GPUs. So, what 
about GPU support?

[Os4ML] automatically uses GPUs if they are available in the Kubernetes 
cluster. Unfortunately, GPUs are known to be a topic of their own. [k3d] describes 
it in their documentation [here][k3d-documentation]. 
If you have problems building the Docker image, remember to install the 
`nvidia-container-toolkit` in addition to the `nvidia-container-runtime`.


[Kubernetes]: https://kubernetes.io/
[k3d]: https://k3d.io
[k3d-documentation]: https://k3d.io/v5.2.2/usage/advanced/cuda/
[Terraform]: https://www.terraform.io/
[Os4ML]: https://github.com/WOGRA-AG/Os4ML
[ArgoCD]: https://github.com/argoproj/argo-cd/
