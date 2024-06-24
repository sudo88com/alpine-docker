# sudo88com/alpine-docker

[![Ansible Docker Build](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_ansible.yml/badge.svg)](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_ansible.yml)
[![Packer Docker Build](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_packer.yml/badge.svg)](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_packer.yml)
[![Packer Docker Build](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_packer.yml/badge.svg)](https://github.com/sudo88com/alpine-docker/actions/workflows/docker_buildx_packer.yml)

This repository contains Dockerfiles for building Alpine-based Docker images for various tools. It is organized into directories, each with its own Dockerfile.

## Overview

This repository is set up to automatically update the Alpine images and rebuild the Docker images using Renovate. Renovate is configured to monitor the Dockerfile in each directory and create pull requests to update them when a new version of Alpine is available.

## Automated Updates with Renovate
This repository uses Renovate to keep the Alpine base images up-to-date. Renovate scans the repository for Dockerfile updates and automatically creates pull requests to update the images when a new version of Alpine is available. The configuration for Renovate is stored in the renovate.json file.

## Renovate Configuration (renovate.json)

The renovate.json file contains the configuration settings for Renovate to manage the Docker image updates. It ensures that the repository always uses the latest version of the Alpine base image, improving security and stability.

# License

This project is licensed under the [MIT License](/LICENSE). See the LICENSE file for details.
