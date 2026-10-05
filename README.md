# AnsibleForms Docker Compose

[![CI](https://img.shields.io/github/actions/workflow/status/ansibleforms/docker/ci.yml?branch=main&label=CI)](https://github.com/ansibleforms/docker/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/license-GPL--3.0-blue)](LICENSE)
[![Docs](https://img.shields.io/badge/docs-ansibleforms.com-informational)](https://ansibleforms.com)

A Docker Compose setup that runs [AnsibleForms](https://github.com/ansibleforms/ansibleforms) 7 with its MySQL
database, sample playbooks and sample forms, so docker and docker compose are all you need to get started.
The full installation guide is at [ansibleforms.com](https://ansibleforms.com/installation).

## Versions

Each branch pins one AnsibleForms major, so a setup never jumps to a new major on its own.
Coming from 6? Read [Upgrading to 7](https://ansibleforms.com/upgrade-7) first.

| Branch | Image |
|---|---|
| `main` | `ghcr.io/ansibleforms/ansibleforms:7` |
| [`v6`](https://github.com/ansibleforms/docker/tree/v6) | `ghcr.io/ansibleforms/ansibleforms:6` |

Images are published to the GitHub Container Registry only; `ansibleguy/ansibleforms` on Docker Hub is no longer updated.

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
- Ansible, Python 3 and a set of Galaxy collections inside the image

## Kubernetes

For Kubernetes, use the Helm chart in [ansibleforms/helm-charts](https://github.com/ansibleforms/helm-charts) instead.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Report security issues as [SECURITY.md](SECURITY.md) describes.

## License

[GPL-3.0](LICENSE).
