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

Every AnsibleForms release also tags this repository as `vX.Y.Z`, so the setup of a version can be taken exactly as it was.

Images live on GHCR only; `ansibleguy/ansibleforms` on Docker Hub is no longer updated.

## Getting started

Clone the repository, review the settings in `.env` (change every password), and start the stack.
The app then listens on https://localhost with a self-signed certificate; log in as `admin` with the `ADMIN_PASSWORD`
of `.env`. While that is still the public default, `AnsibleForms!123`, the app first asks you to choose a new password.

```bash
git clone https://github.com/ansibleforms/docker.git ansibleforms
cd ansibleforms
sudo chown -R 1000:1000 data
docker compose up -d
```

The app and the RTE run as the user `node` (uid 1000), so they need to own `data/`: that is what the `chown` is for.
Coming from 6, whose container ran as root, run the same `chown` once before you start 7; MySQL takes its own folder back when it starts.

## What you get

Everything under `data/` is mounted into the containers and survives a restart or an upgrade.

- A demo `config.yaml` with categories, roles and constants, and sample forms
- Sample maintenance playbooks and a `dummy.yaml` playbook
- Sample custom JavaScript functions and jq definitions to extend AnsibleForms
- An RTE container that runs the playbooks, with ansible, Python 3 and a set of Galaxy collections
- A config seed, `data/seed.yaml`, that registers the RTE as the default runner

## Database

The app and the RTE connect to MySQL as `ansibleforms` (`MYSQLDB_USER` in `.env`), with all rights on the `AnsibleForms`
schema and none elsewhere: a hole in the app then stays a hole in its own data. Root (`MYSQLDB_ROOT_PASSWORD`) is for MySQL.

MySQL creates that user on its first start only. An install that has connected as root so far keeps its database, so
create the user once, with the password you set in `MYSQLDB_PASSWORD`, before you start it with this `.env`:

```bash
docker compose up -d mysqldb
docker compose exec mysqldb mysql -uroot -p -e "CREATE USER 'ansibleforms'@'%' IDENTIFIED BY '<MYSQLDB_PASSWORD>';
  GRANT ALL PRIVILEGES ON AnsibleForms.* TO 'ansibleforms'@'%';"
```

## Running playbooks

AnsibleForms 7 runs no playbook in the app: the `rte` container runs them, from
`ghcr.io/ansibleforms/ansibleforms-rte-full:7`. The app reaches it on `http://rte:8000` with `RTE_TOKEN` from `.env`.

`data/seed.yaml` registers it as the default runner on every start, so it is read-only under Connections > Runners.
Ansible settings, roles and collections under `data/ansible/` are mounted into the RTE, not the app. When your
playbooks need more, build an image FROM `ansibleforms-rte-core` or `ansibleforms-rte-full` and point the `rte` service
at it: the app's [examples/rte](https://github.com/ansibleforms/ansibleforms/tree/main/examples/rte) shows how.

## Kubernetes

For Kubernetes, use the Helm chart in [ansibleforms/helm-charts](https://github.com/ansibleforms/helm-charts) instead.

## Contributing

Contributions are welcome. Start with these files:

- [CONTRIBUTING.md](CONTRIBUTING.md): how to propose a change and open a pull request
- [SECURITY.md](SECURITY.md): how to report a security issue

## License

[GPL-3.0](LICENSE).
