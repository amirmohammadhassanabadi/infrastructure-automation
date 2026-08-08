# Report Generator

An Ansible role responsible for generating human-readable infrastructure reports from collected host and Kubernetes information.

## Responsibilities

The role:

* Creates the report output directory.
* Renders the infrastructure report template.
* Generates one report per managed host.

## Current Report Sections

The report currently contains:

* Host information
* CPU
* Memory
* Storage
* Network interfaces
* Kubernetes information
* Kubernetes node roles
* Kubernetes components

## Role Structure

```text
report_generator/
├── defaults/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
│   └── report.txt.j2
└── README.md
```

## Configuration

The report output directory can be configured using:

```yaml
report_output_dir: "{{ playbook_dir }}/../reports"
```

## Usage

```yaml
- hosts: all
  roles:
    - report_generator
```

## Design

The role is intentionally separated from the inventory collection roles.

Collection roles are responsible for gathering information, while this role is responsible for presenting that information as a report.

Additional report formats may be added in the future.
