# Intro

> **Note:**  
> This is the setup for AnsibleForms 7. It pins the image to `ghcr.io/ansibleforms/ansibleforms:7`, so it
> gets every 7.x release and never jumps to a new major version on its own. For AnsibleForms 6,
> use the [`v6` branch](https://github.com/ansibleforms/docker/tree/v6). Coming from 6? Read
> [Upgrading to 7](https://ansibleforms.com/upgrade-7) first.

This project is a simple docker-compose to quickly get you started with AnsibleForms.
The docker compose will spin up the mysql database and grab the latest AnsibleForms 7.x image from the GitHub Container Registry.
The same image is also on Docker Hub as `ansibleguy/ansibleforms`. Use that name instead if you prefer.
It will install everything with defaults and present a dummy playbook as well as a demo config.yaml file and sample forms.
The Ansibleforms image comes with Ansible and Python3 (and some galaxy collections), so apart from docker and docker compose there are no prerequisites.

# How to Install
Simply follow the instructions on (https://ansibleforms.com)

# Data Contents
* sample maintenance playbooks
* sample maintenance forms
* dummy.yaml playbook
* sample custom functions to extend Ansible Forms.

# K8S
Searching for K8S install, find the helm install here.  
(https://github.com/ansibleforms/ansibleforms-helm)



