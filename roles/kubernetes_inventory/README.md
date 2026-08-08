# Kubernetes Inventory

An Ansible role for detecting and collecting Kubernetes information directly from managed Kubernetes nodes.

## Responsibilities

The role currently detects:

* Whether Kubernetes is installed.
* Kubernetes distribution.
* Kubernetes version.
* Kubernetes node roles.
* Kubernetes control-plane components.

## Supported Distributions

Currently supported:

* RKE1
* RKE2

## Detection Approach

The role intentionally performs node-local detection.

It does not require:

* `kubectl`
* A kubeconfig file
* Access to the Kubernetes API

### RKE2

RKE2 is detected using the RKE2 binary and systemd services.

Version information is collected using the RKE2 binary.

### RKE1

RKE1 is detected using Docker-based Kubernetes components.

The Kubernetes version is collected from the kubelet Docker container.

## Collected Data

The role stores Kubernetes information in a structured dictionary:

```yaml
kubernetes:
  installed: true
  distribution: RKE1
  version: v1.x.x
  raw_version: ...
  node_roles:
    - control-plane
    - worker
  components:
    - kube-apiserver
    - kube-controller-manager
    - kube-scheduler
    - etcd
```

## Role Structure

```text
kubernetes_inventory/
├── tasks/
│   ├── main.yml
│   ├── detect.yml
│   ├── version.yml
│   ├── node_role.yml
│   ├── components.yml
│   └── report.yml
└── README.md
```

## Usage

```yaml
- hosts: kubernetes
  roles:
    - kubernetes_inventory
```

## Current Limitations

The role currently focuses on RKE1 and RKE2.

Additional Kubernetes distributions and deeper cluster-level inventory may be added in future versions.
