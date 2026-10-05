# Intro

> **Note:**  
> This branch is for AnsibleForms 6. It pins the image to `ghcr.io/ansibleforms/ansibleforms:6`, so it
> keeps getting 6.x patch releases and never moves to 7. The `main` branch is the setup for
> the current version.

This project is a simple docker-compose to quickly get you started with AnsibleForms.
The docker compose will spin up the mysql database and grab the latest AnsibleForms 6.x image from the GitHub Container Registry.
Images are published there only: the old Docker Hub repository (`ansibleguy/ansibleforms`) is no longer updated.
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
(https://github.com/ansibleforms/helm-charts)



