# Infrastructure Automation

An Ansible-based infrastructure inventory and automation project designed to collect information from Linux servers, Kubernetes nodes, and network infrastructure, then generate structured infrastructure reports.

The project is being developed with a modular role-based architecture so that individual automation tasks can be reused and extended independently.

## Project Goals

The main goals of this project are:

* Collect operating system and hardware information.
* Collect network interface and storage information.
* Detect Kubernetes installations.
* Identify Kubernetes distributions such as RKE1 and RKE2.
* Collect Kubernetes version information.
* Identify Kubernetes node roles.
* Detect Kubernetes control-plane components.
* Generate infrastructure reports.
* Automate Cisco switch configuration backups.
* Keep infrastructure automation modular and reusable.

## Architecture

```text
                         Infrastructure
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
        Linux Hosts      Kubernetes Nodes   Cisco Switches
             │                │                │
             ▼                ▼                ▼
       os-reporter    kubernetes_inventory   Cisco roles
             │                │                │
             └────────────────┼────────────────┘
                              │
                              ▼
                       report_generator
                              │
                              ▼
                           reports/
```

## Repository Structure

```text
infrastructure-automation/
│
├── inventories/
│   └── ...
│
├── playbooks/
│   └── ...
│
├── roles/
│   ├── os-reporter/
│   ├── kubernetes_inventory/
│   ├── report_generator/
│   └── cisco_backup/
│
├── reports/
│   └── ...
│
├── backups/
│   └── ...
│
├── ansible.cfg
├── requirements.yml
└── README.md
```

## Roles

### `os-reporter`

Collects operating-system and hardware information from managed Linux hosts.

Current information includes:

* Hostname
* FQDN
* Operating system
* Kernel
* Architecture
* CPU information
* Memory
* Swap
* Mounted filesystems
* Network interfaces
* IPv4 addresses
* IPv6 addresses

### `kubernetes_inventory`

Detects and inventories Kubernetes installations running on managed hosts.

Current capabilities include:

* Detect whether Kubernetes is installed.
* Detect RKE1.
* Detect RKE2.
* Collect Kubernetes version.
* Detect Kubernetes node roles.
* Detect Kubernetes control-plane components.

The role currently focuses on node-local detection and does not require `kubectl` or a kubeconfig.

### `report_generator`

Generates human-readable infrastructure reports from the information collected by the other roles.

The report currently contains:

* Host information
* CPU information
* Memory information
* Storage information
* Network interfaces
* Kubernetes information
* Kubernetes node roles
* Kubernetes components

### `cisco_backup`

Automates Cisco IOS configuration backups using Ansible network modules.

Current functionality includes:

* Retrieve the running configuration.
* Save configurations locally.
* Organize backups by device.

## Example Report

A generated report contains information similar to:

```text
# Infrastructure Report

## Host Information

Inventory Name    : ubuntu
Hostname          : ubuntu
FQDN              : ubuntu.example.local
Operating System  : Ubuntu 24.04 LTS
Kernel            : 6.8.0
Architecture      : x86_64

## CPU

Model             : Intel(R) Xeon(R) CPU
Sockets           : 1
Cores / Socket    : 4
Logical CPUs      : 4

## Memory

Total RAM         : 8.00 GB
Total Swap        : 2.00 GB

## Kubernetes

Installed         : true
Distribution      : RKE2
Version           : v1.35.x+rke2r1

### Node Roles

- control-plane
- worker

### Components

- kube-apiserver
- kube-controller-manager
- kube-scheduler
- etcd
```

## Requirements

* Ansible
* Python
* SSH access to managed Linux hosts
* Appropriate privileges on managed hosts
* Docker access for RKE1 detection
* Cisco Ansible collections for network automation

## Design Principles

This project follows several principles:

1. **Modularity**
   Infrastructure functionality is separated into independent Ansible roles.

2. **Local detection where possible**
   Kubernetes inventory is collected from the node itself instead of depending on `kubectl` and kubeconfig files.

3. **Separation of collection and presentation**
   Inventory roles collect information, while the report generator is responsible for presenting it.

4. **Idempotent automation**
   Tasks should be safe to execute repeatedly without producing unnecessary changes.

5. **Extensibility**
   New infrastructure technologies should be added as independent roles rather than tightly coupling them to existing roles.

## Project Status

🚧 This project is under active development.

Current focus:

* Linux infrastructure inventory
* Kubernetes inventory
* Infrastructure report generation
* Cisco configuration backup automation

Future improvements will include additional infrastructure checks, improved validation, additional report formats, and broader platform support.