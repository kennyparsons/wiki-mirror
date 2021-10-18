---
title: Docker Blueprint
description: 
published: true
date: 2021-10-18T19:11:03.223Z
tags: 
editor: markdown
dateCreated: 2020-09-29T14:58:05.023Z
---

# Docker Blueprint
A complete guide to setting up Docker and Docker-Compose from scratch.

## Prerequisites
- Debian 10
- root/sudo for the installation
 
## Installation
Install the dependencies:
```bash
sudo apt update &&
  sudo apt install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common
```

Add the Docker repository signature key:
```bash
curl -sSL https://download.docker.com/linux/debian/gpg | sudo apt-key --keyring /etc/apt/trusted.gpg.d/docker.gpg add -
```

Add the Debian Docker repository:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/trusted.gpg.d/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
```

Install Docker:
```bash
sudo apt update && sudo apt install -y docker-ce
```

## Non-Root Docker Execution
To configure Docker to run without sudo or root, follow these config steps. Note: This now assumes you are logged in as a non-root user.

Add the current user to the docker group:
```bash
sudo usermod -aG docker "${USER}"
```

Apply the new group membership:
```bash
su - "${USER}"
```

Verify membership with:
```bash
id -nG
```

If the ouput includes `docker`, then the process is complete. Docker is ready to go.

# Docker Compose

## Prerequisites
 - Docker installed (see above)
 - Docker-Compose latest version number (e.g. 1.27.4)
 - root/sudo for the installation
 
## Installation
Get the latest docker-compose version number [here](https://github.com/docker/compose/releases). At the time of this writing, it is 1.27.4. 

Next, use that version number to install docker-compose:
```bash
DC_VERSION=1.29.2 &&
  sudo curl -L https://github.com/docker/compose/releases/download/"${DC_VERSION}"/docker-compose-Linux-x86_64 -o /usr/local/bin/docker-compose &&
  sudo chmod +x /usr/local/bin/docker-compose
```

Confirm that the installation completed successfully:
```bash
docker-compose --version
```

The ouput should display the version and build information. 