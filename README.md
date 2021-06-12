# Execution Environment for Ansible Anwendertreffen Demo

This repository contains the files necessary to build the Ansible Execution Environment for running the Playbook used in the Live Demo from my presentation at the second "Ansible Anwendertreffen" conference.  
The execution environment and Playbooks used in the Demo provision and configure a k3s Kubernetes cluster and deploy the Kubernetes Dashboard on top of it.   
The playbooks can be found in a seperate repository: https://github.com/TimGrt/ansible-anwendertreffen-demo-playbooks  
The pre-build container can be found in and pulled from my Docker Hub Repository: https://hub.docker.com/r/timgrt/ansible-anwendertreffen-demo-ee  
Building and running the execution environment requires two Python packages, as well as a container-runtime. 
I used Docker to build the execution environment container image and Podman to run the container on a sperate host.

[![Docker Build and Publish](https://github.com/TimGrt/ansible-anwendertreffen-demo-execution-environment/actions/workflows/ci.yml/badge.svg)](https://github.com/TimGrt/ansible-anwendertreffen-demo-execution-environment/actions/workflows/ci.yml) ![Docker Pulls](https://img.shields.io/docker/pulls/timgrt/ansible-anwendertreffen-demo-ee) ![CodeFactor Grade](https://img.shields.io/codefactor/grade/github/timgrt/ansible-anwendertreffen-demo-execution-environment/main)

## Tags

The following tags are available:
* `latest`

## Requirements

The following requirements are necessary to build and/or run the execution environment.  

1. Install a container runtime, currently Podman and Docker are supported.
2. Install ansible-builder.
```bash
pip3 install ansible-builder==1.0.0.0a1
```
3. Install ansible-runner (only Version >= 2.0 is able to run execution environments, currently, this is not latest).  
```bash
pip3 install ansible-runner==2.0.0a2
```

## Build the execution environment

This builds the execution environment container with the Docker container-runtime.
```bash
ansible-builder build --container-runtime docker --tag ansible-anwendertreffen-demo-ee 
```
For building the image only the `execution-environment.yml`, `requirements.yml` and `requirements.txt` are necessary.  
The _context_ folder will be created by ansible-builder, it is left here because the resulting _Dockerfile_ is used for building the image in the Docker Hub repository.

## Run playbook with execution environment

This runs the playbook with the podman container-runtime. The container image used was pulled from DockerHub before.
```bash
ansible-runner playbook --container-image timgrt/ansible-anwendertreffen-demo-ee --inventory hosts k3s-install.yml
```

## Author

Created 2021 by Tim Grützmacher
