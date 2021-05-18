# Execution Environment for Ansible Anwendertreffen Demo

This repository contains the files necessary to build the Ansible Execution Environment for running the Playbook used in the Live Demo from my presentation at the second "Ansible Anwendertreffen" conference.  
The Playbooks used in the Demo provision and configure a k3s Kubernetes cluster and deploy the Kubernetes Dashboard on top of it. The playbooks can be found in a seperate repository:
https://github.com/TimGrt/ansible-anwendertreffen-demo-playbooks
Building and running the execution environment requires two Python packages, as well as a container-runtime. I used Docker to build to execution environment container image and Podman to run the container on a sperate host.

## Requirements

Install ansible-builder.
```bash
pip3 install ansible-builder==2.0.0a2
```

Install ansible-runner.
```bash
pip3 install ansible-runner==1.0.0.0a1
```

## Run playbook with execution environment

This runs the playbook with the podman container-runtime.
```bash
ansible-runner playbook --container-image timgrt/ansible-anwendertreffen-demo-ee --inventory hosts k3s-install.yml
```
