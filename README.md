# sudo88com/alpine-docker

[![Ansible Docker Build](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_ansible.yml/badge.svg)](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_ansible.yml)
[![Packer Docker Build](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_packer.yml/badge.svg)](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_packer.yml)
[![Terraform Docker Build](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_terraform.yml/badge.svg)](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_terraform.yml)

This repository contains Dockerfiles for building Alpine-based Docker images for various tools. It is organized into directories, each with its own Dockerfile.

## Overview

This repository is set up to automatically update the Alpine images and rebuild the Docker images using Renovate. Renovate is configured to monitor the Dockerfile in each directory and create pull requests to update them when a new version of Alpine is available.

# License

This project is licensed under the [MIT License](/LICENSE). See the LICENSE file for details.
