# AnsibleForms Docker Compose

[![CI](https://img.shields.io/github/actions/workflow/status/ansibleforms/docker/ci.yml?branch=main&label=CI)](https://github.com/ansibleforms/docker/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/license-GPL--3.0-blue)](LICENSE)
[![Docs](https://img.shields.io/badge/docs-ansibleforms.com-informational)](https://ansibleforms.com)

A Docker Compose setup that runs [AnsibleForms](https://github.com/ansibleforms/ansibleforms) with its MySQL
database, sample playbooks and sample forms, so docker and docker compose are all you need to get started.
The full installation guide is at [ansibleforms.com](https://ansibleforms.com/installation).

## Versions

Each branch pins one AnsibleForms major, so a setup never jumps on its own; read [Upgrading to 7](https://ansibleforms.com/upgrade-7) before moving up.

| Branch | Image |
|---|---|
| `main` | `ghcr.io/ansibleforms/ansibleforms:7` |
| [`v6`](https://github.com/ansibleforms/docker/tree/v6) | `ghcr.io/ansibleforms/ansibleforms:6` |

Images live on GHCR only; `ansibleguy/ansibleforms` on Docker Hub is no longer updated.

## Getting started

Clone the repository, review the settings in `.env` (change every password), and start the stack.
The app then listens on https://localhost with a self-signed certificate; log in as `admin`.

```bash
git clone https://github.com/ansibleforms/docker.git ansibleforms
cd ansibleforms
docker compose up -d
```

## What you get

Everything under `data/` is mounted into the containers and survives a restart or an upgrade.

- A demo `config.yaml` with categories, roles and constants, and sample forms
- Sample maintenance playbooks and a `dummy.yaml` playbook
- Sample custom JavaScript functions and jq definitions to extend AnsibleForms
- An RTE container that runs the playbooks, with ansible, Python 3 and a set of Galaxy collections
- A config seed, `data/seed.yaml`, that registers the RTE as the default runner

## Running playbooks

AnsibleForms 7 runs no playbook in the app: the `rte` container runs them, from
`ghcr.io/ansibleforms/ansibleforms-rte:7`. The app reaches it on `http://rte:8000` with `RTE_TOKEN` from `.env`.

`data/seed.yaml` registers it as the default runner on every start, so it is read-only under Connections > Runners.
Ansible settings, roles and collections under `data/ansible/` are mounted into the RTE, not the app. When your
playbooks need more, build an image from the app's `Dockerfile.rte` and point the `rte` service at it.

## Kubernetes

For Kubernetes, use the Helm chart in [ansibleforms/helm-charts](https://github.com/ansibleforms/helm-charts) instead.

## Contributing

Contributions are welcome. Start with these files:

- [CONTRIBUTING.md](CONTRIBUTING.md): how to propose a change and open a pull request
- [SECURITY.md](SECURITY.md): how to report a security issue

## License

[GPL-3.0](LICENSE).
