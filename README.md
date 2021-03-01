# Debian 10 (Buster) Ansible Test Image

[![CI](https://github.com/jwaibel/docker-ansible-debian10/workflows/Build/badge.svg?branch=master&event=push)](https://github.com/jwaibel/docker-ansible-debian10/actions?query=workflow%3ABuild) [![Docker pulls](https://img.shields.io/docker/pulls/jwaibel/docker-ansible-debian10)](https://hub.docker.com/r/jwaibel/docker-ansible-debian10/)

Debian 10 (Buster) Docker container for Ansible/DebOps playbook and role testing.

>**Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and performant production environment. Use on production servers at your own risk!


## Tags
  - `latest`: Latest stable version of Ansible, with Python 3.x.

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `master` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. `cd` into this directory.
  3. Run `docker build -t debian10-ansible .`

> Note: Switch between `master`,`testing` and `debops` depending on whether you want the extra testing tools or a preinstalled DebOps environment present in the resulting image.

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull jwaibel/docker-ansible-debian-10:latest` (or use the image you built earlier, e.g. `debian10-ansible`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro jwaibel/docker-ansible-debian10:latest` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Jenkins and Travis. This container allows me to test roles and playbooks using Ansible running locally inside the container.

## Author

2021 J. Waibel <j.waibel@juergen-waibel.de>

> Note this is based on the great work of Jeff Gerling (https://github.com/geerlingguy) and adopted to my own needs

