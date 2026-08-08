# OS Reporter

An Ansible role for collecting operating-system, hardware, storage, and network information from Linux hosts.

## Responsibilities

The role collects:

* Hostname
* FQDN
* Operating system
* Kernel version
* CPU information
* Memory
* Swap
* Mounted filesystems
* Network interfaces
* IPv4 addresses
* IPv6 addresses

## Role Structure

```text
os-reporter/
├── tasks/
│   ├── main.yml
│   ├── collect.yml
│   └── report.yml
├── templates/
│   └── report.txt.j2
└── README.md
```

## Usage

Include the role in a playbook:

```yaml
- hosts: linux
  roles:
    - os-reporter
```

The collected information is made available to the report generation stage.

## Notes

The role is designed to collect infrastructure information rather than modify the managed systems.
