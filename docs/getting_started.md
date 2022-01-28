# Getting Started
We try to keep things as simple as possible. 

## Prerequisites
In fact, all it takes is a running [Kubernetes][] cluster to get started.
With [k3d][] you can do it like this, for example

```sh
k3d cluster create os4ml-cluster
```

If you want to do machine learning, GPUs are always an issue. Unfortunately, 
GPUs are known to be a topic of their own. For more information on how to 
use GPUs please read the [support for k3d](gpu_support/k3d.md) or the [support 
for MicroK8s](gpu_support/microk8s.md).

## Installation
Nobody wants complicated installations. We neither. For this reason
we provide [Terraform][] scripts to install Os4ML on any [Kubernetes][]
cluster. And this is how it works:

```sh
git clone https://github.com/WOGRA-AG/Os4ML.git
cd os4ml/terraform
terraform init
terraform apply -auto-approve
```

This takes a bit and offers the opportunity to get a coffee.

## Usage
You won't believe it, but in fact your [Kubernetes][] cluster now hosts Os4ML 
including a fully functional [Kubeflow][]. And that's how you get it:

```sh
kubectl port-forward -n istio-system svc/istio-ingressgateway 8000:80
```
Now, open `localhost:8000` for [Kubeflow][] or `localhost:8000/os4ml/` for 
Os4ML (don't forget the slash). As described 
[here](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/),
the connection is terminated when the command is aborted. Whenever you are 
asked for credentials, there exists a standard user with email 
`user@example.com` and password `12341234`.

[Kubernetes]: https://kubernetes.io/
[Kubernetes/port-forward]: https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/
[Kubeflow]: https://www.kubeflow.org/
[k3d]: https://k3d.io
[Terraform]: https://www.terraform.io/
