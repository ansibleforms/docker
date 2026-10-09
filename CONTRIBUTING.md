# Contributing to the AnsibleForms docker setup

Thanks for helping out. This repository is the docker-compose setup that runs AnsibleForms
with its MySQL database. The application itself lives in
[ansibleforms/ansibleforms](https://github.com/ansibleforms/ansibleforms).

## Table of contents

- [What lives where](#what-lives-where)
- [Branches](#branches)
- [Pull requests](#pull-requests)
- [Trying a change](#trying-a-change)

---

## What lives where

The setup is a compose file, its settings and the data the containers start with.

| Path | Holds |
|---|---|
| `docker-compose.yml` | the AnsibleForms, RTE and MySQL containers and their volumes |
| `.env` | the settings, with sample values that work out of the box |
| `data/` | what AnsibleForms and MySQL start with: config, sample forms and playbooks, custom functions, ansible and git settings, and the config seed that registers the RTE |

What the containers write at runtime (the database, logs, backups, keys) also lands in
`data/`, and `.gitignore` keeps it out of git.

---

## Branches

Each AnsibleForms major version has its own branch, and the image tag in
`docker-compose.yml` is pinned to that major.

| Branch | AnsibleForms | Image |
|---|---|---|
| `main` | 7 | `ghcr.io/ansibleforms/ansibleforms:7` |
| `v6` | 6 | `ghcr.io/ansibleforms/ansibleforms:6` |

Open a change against the branch of the version it is for. A fix that applies to both goes
to each branch in a pull request of its own.

---

## Pull requests

`main` and `v6` are protected: everything reaches them through a pull request, and pull
requests are **squash-merged**.

1. Branch from the target branch, named `<type>/<short-description>`, for example
   `fix/mysql-port`.
2. Give the pull request a [Conventional Commits](https://www.conventionalcommits.org/)
   title, for example `fix: expose MySQL on the documented port`.
3. The **Title** and **Branch** checks must pass.

Dependabot keeps the image tags up to date within their major version.

---

## Trying a change

Start the setup from a clean copy, so leftovers from an earlier run cannot hide a problem:

```bash
git clone -b <your-branch> https://github.com/ansibleforms/docker.git try && cd try
docker compose up -d
```

AnsibleForms answers on `https://localhost` (the port is `WEBAPP_LOCAL_PORT` in `.env`).
Remove it again with `docker compose down -v` and by deleting the folder.
