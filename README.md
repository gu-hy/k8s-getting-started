# Start

## What is K8s

Simply - container orchestrator (declarative configuration + automation)

### Containers

[K8s Overwiev](https://kubernetes.io/docs/concepts/overview/)

```mermaid
flowchart TD
    a[App1]<-->D
    B[App2]<-->D
    C[App3]<-->D
    D(OS)<-->E
    E(Hardware)
```

```mermaid
flowchart TD
    A[App1]<-->A1
    A1[Libs1 / OS / VM]<-->E
    B[App2]<-->B1
    B1[Libs2 / OS2 / VM]<-->E
    C[App3]<-->C1
    C1[Libs3 / OS3 / VM]<-->E
    E(Hypervisor)<-->F
    F(OS)<-->G
    G(Hardware)
```

```mermaid
flowchart TD
    A[App1]<-->A1
    A1[Libs/OS]<-->A2
    A2[Container1]<-->E
    B[App2]<-->B1
    B1[Libs2/OS2]<-->B2
    B2[Container2]<-->E
    C[App3]<-->C1
    C1[Libs3/OS3/VM]<-->C2
    C2[Container3]<-->E
    E(CRI)<-->F
    F(OS)<-->G
    G(Hardware)
```

- Containers are similar to VMs, but they share OS properties (kernel) among the applications.
- Containers provides isolation of user space
- Containers are portable. Bundled libraries and apps are build into container

### CRI (Container Runtime Interface)

[About CRI](https://www.aquasec.com/cloud-native-academy/container-security/container-runtime-interface/)
The container engine (often referred to as operating-system-level virtualization) is based on an operating system in which the kernel allows multiple isolated instances. Each instance is called a container, virtualization engine, or “jail”.

Container runtime interface (CRI) is a plugin interface that lets the kubelet an agent that runs on every node in a Kubernetes cluster use more than one type of container runtime. Container runtimes are a foundational component of a modern containerized architecture.

### Why K8s need CRI

- kubelet - the kubelet is a daemon that runs on every Kubernetes node. It implements the pod and node APIs that drive most of the activity within Kubernetes.
- Pods - a pod is the smallest unit of reference within Kubernetes. Each pod runs one or more containers, which together form a single functional unit.
- Pod specs - the kubelet read pod specs, usually defined in YAML configuration files. The pod specs say which container images the pod should run. It provides no details as to how containers should run - for this, Kubernetes needs a container runtime.
- Container runtime - a Kubernetes node must have a container runtime installed. When the kubelet wants to process pod specs, it needs a container runtime to create the actual containers. The runtime is then responsible for managing the container lifecycle and communicating with the operating system kernel.

### Runc and OCI

[Open Container Initiative](https://opencontainers.org/about/overview/)
[Runc](https://github.com/opencontainers/runc)

- runc is a CLI tool for spawning and running containers on Linux according to the OCI specification - a seed container runtime engine. The majority of modern container runtime environments use runc and develop additional functionality around this seed engine.
- OCI image specification-OCI adopted the original Docker image format as the basis for the OCI image specification. The majority of open source build tools support this format, including BuildKit, Podman, and Buildah. Container runtimes that implement the OCI runtime specification can unbundle OCI images and run its content as a container.

## How does K8s Realy work

![K8s Cluster Overview](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)

### K8s object

- Pod - Pods are the smallest deployable units of computing that you can create and manage in Kubernetes. A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.
- Service - In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster.
- ReplicaSet - A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.
- DaemonSet - A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.
- Deployment - Describes the desired state and makes sure to change the actual state to the desired state if needed. A deployment manages Pods and ReplicaSets so you don’t have to.

## Minikube

### Install and run

[Install minikube](https://minikube.sigs.k8s.io/docs/start/)

[Hello Minikube (world)](https://kubernetes.io/docs/tutorials/hello-minikube/)
