# GPU support with MicroK8s

Canonical promotes [MicroK8s](https://microk8s.io/) as 'Low-ops, minimal 
production Kubernetes, for devs, cloud, clusters, workstations, Edge and 
IoT'. GPU support is provided as add-on using th command `microk8s enable 
gpu` as described [here](https://microk8s.io/docs/addon-gpu).

Unfortunately, this fails from time to time. In the following we describe 
an alternative procedure to enable gpu support for microk8s. Unfortunately,
due to time constraints, the instructions cannot be continuously updated. 
Please let us know if something is no longer up to date so that this can 
be adjusted accordingly.

## Install MicroK8s
Be sure no MicroK8s is installed, otherwise use `sudo snap remove microk8s --purge`.

Install MicroK8s on Linux

```bash
sudo snap install microk8s --classic
```

Check the status while Kubernetes starts

```bash
microk8s status --wait-ready
```

Enable DNS support

```bash
microk8s enable dns
```

## Enable GPU support in microk8s
Now we are adapting the following [article](https://dev.to/mweibel/add-nvidia-gpu-support-to-k3s-with-containerd-4j17).

Add a demonset to the node which is responsible to enable gpu capacity (nvidia.com/gpu) for every node it is done once.

```bash
microk8s kubectl apply -f https://raw.githubusercontent.com/kubernetes/kubernetes/release-1.14/cluster/addons/device-plugins/nvidia-gpu/daemonset.yaml
```
Add a label to the node for gpu support

```bash
microk8s kubectl label nodes DEVICE_NAME cloud.google.com/gke-accelerator=true
```
## Bugfix containerd gpu support for microk8s
To enable the nvidia-conatiner-runtime in containerd edit the two files

```bash
sudo vim /var/snap/microk8s/current/args/containerd-template.toml
sudo vim /var/snap/microk8s/current/args/containerd.toml
```
And replace
```toml
    # 'plugins."io.containerd.grpc.v1.cri".containerd.runtimes' is a map from CRI RuntimeHandler strings, which specify types
    # of runtime configurations, to the matching configurations.
    # In this example, 'runc' is the RuntimeHandler string to match.
    [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
      # runtime_type is the runtime type to use in containerd e.g. io.containerd.runtime.v1.linux
      runtime_type = "io.containerd.runc.v1"

    [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.nvidia-container-runtime]
      # runtime_type is the runtime type to use in containerd e.g. io.containerd.runtime.v1.linux
      runtime_type = "io.containerd.runc.v1"

      [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.nvidia-container-runtime.options]
        BinaryName = "nvidia-container-runtime"

```

with

```toml
    # 'plugins."io.containerd.grpc.v1.cri".containerd.runtimes' is a map from CRI RuntimeHandler strings, which specify types
    # of runtime configurations, to the matching configurations.
    # In this example, 'runc' is the RuntimeHandler string to match.
    [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
      # runtime_type is the runtime type to use in containerd e.g. io.containerd.runtime.v1.linux
      runtime_type = "io.containerd.runc.v1"

      [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
        BinaryName = "nvidia-container-runtime"

    [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.nvidia-container-runtime]
      # runtime_type is the runtime type to use in containerd e.g. io.containerd.runtime.v1.linux
      runtime_type = "io.containerd.runc.v1"

      [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.nvidia-container-runtime.options]
        BinaryName = "nvidia-container-runtime"
```
With this setting every container executed by containerd has gpu support, 
but that is for our use case fine.

## Ensure nvidia driver is loaded and device files are ready
Use the script from [here](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile-verifications).

```bash
touch enable-dev-nvida.sh
vim enable-dev-nvida.sh
```

Add this code

```bash
#!/bin/bash

/sbin/modprobe nvidia

if [ "$?" -eq 0 ]; then
  # Count the number of NVIDIA controllers found.
  NVDEVS=`lspci | grep -i NVIDIA`
  N3D=`echo "$NVDEVS" | grep "3D controller" | wc -l`
  NVGA=`echo "$NVDEVS" | grep "VGA compatible controller" | wc -l`

  N=`expr $N3D + $NVGA - 1`
  for i in `seq 0 $N`; do
    mknod -m 666 /dev/nvidia$i c 195 $i
  done

  mknod -m 666 /dev/nvidiactl c 195 255

else
  exit 1
fi

/sbin/modprobe nvidia-uvm

if [ "$?" -eq 0 ]; then
  # Find out the major device number used by the nvidia-uvm driver
  D=`grep nvidia-uvm /proc/devices | awk '{print $1}'`

  mknod -m 666 /dev/nvidia-uvm c $D 0
else
  exit 1
fi
```
And execute the script

```bash
chmod +x enable-dev-nvida.sh
sudo ./enable-dev-nvida.sh
```
Also check that Nvidia and Cuda is present

```
nvidia-smi
```

Sample output
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.63.01    Driver Version: 470.63.01    CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:3B:00.0 Off |                  N/A |
| N/A   54C    P0    N/A /  N/A |    249MiB /  2002MiB |     10%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
```

## Restart MicroK8s and get node information

```bash
microk8s stop && microk8s start && microk8s status --wait-ready
microk8s kubectl describe node
```

You should now get `nvidia.com/gpu` capacity like this

```
Capacity:
  cpu:                8
  ephemeral-storage:  473841544Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  memory:             16030004Ki
  nvidia.com/gpu:     1
  pods:               110
```

## Test pod with GPU capabilities

To test the gpu support we create a simple deployment yaml file

```bash
vim test-gpu.yaml
```

with content

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cuda-vector-add
spec:
  restartPolicy: OnFailure
  containers:
    - name: cuda-vector-add
      image: "k8s.gcr.io/cuda-vector-add:v0.1"
      resources:
        limits:
          nvidia.com/gpu: 1
        requests:
          nvidia.com/gpu: 1
```

Now start the deployment and look for the results. This can take some time 
to  pull the image.

```bash
sudo microk8s kubectl apply -f test-gpu.yaml
microk8s kubectl describe pod cuda-vector-add
microk8s kubectl logs cuda-vector-add
```
The successful log output shows that the GPU is working and can now be used.

```
[Vector addition of 50000 elements]
Copy input data from the host memory to the CUDA device
CUDA kernel launch with 196 blocks of 256 threads
Copy output data from the CUDA device to the host memory
Test PASSED
Done
```