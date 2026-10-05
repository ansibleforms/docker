# Security Policy

This repository is a docker-compose setup for AnsibleForms, so security problems almost
always belong to the application. Please follow the
[AnsibleForms security policy](https://github.com/ansibleforms/ansibleforms/security/policy)
and report privately through its
**[Report a vulnerability](https://github.com/ansibleforms/ansibleforms/security/advisories/new)** page.

**Please do not open a public issue for a security problem.**

If the problem is in this setup itself, for example a default that exposes something it
should not, use **[Report a vulnerability](https://github.com/ansibleforms/docker/security/advisories/new)**
on this repository instead.

The `.env` file ships with sample passwords so the setup starts out of the box. Change
them, and set `ENCRYPTION_SECRET` and `ACCESS_TOKEN_SECRET`, before exposing an install.
