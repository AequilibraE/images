# AequilibraE CI Docker Images

This repository contains Docker configurations for building CI environments for [AequilibraE](https://github.com/AequilibraE/aequilibrae).

## Overview

- **`Dockerfile-windows-ci`**: Builds a CI environment based on Windows Server Core LTSC 2022.
- **`Dockerfile-ubuntu-ci`**: Builds a CI environment based on Ubuntu 24.04.
- Both configurations include:
  - Multi-Python version management with [`uv`](https://astral.sh/uv/).
  - SpatiaLite support.
  - Installation of required dependencies for AequilibraE.
  
## Installed software locations

- **SpatiaLite**:
  - `Ubuntu`: Installed system-wide and available at `/usr/lib/x86_64-linux-gnu/mod_spatialite.so`.
  - `Windows`: Extracted to `C:\spatialite` and added to the system `PATH`.
  
- **Python Virtual Environments**:
  - `Ubuntu`: Created in the project root as `venv-py39`, `venv-py310`, etc. Activate using `. venv-name/bin/activate`.
  - `Windows`: Created in the project root as `venv-py39`, `venv-py310`, etc. Activate using `venv-name\Scripts\activate`.

- **Build Tools (Windows only)**:
  - Visual Studio Build Tools 2022 are installed at `C:\BuildTools` with the native desktop workload.

- **7zip (Windows only)**:
  -  7-Zip is installed at `C:\Program Files\7-Zip`.

## GitHub Actions Workflow

The `build.yml` workflow:
1. Builds the Docker images for both Windows and Ubuntu.
2. Tags each image with the latest AequilibraE release.
3. Pushes the images to the [GitHub Container Registry](https://ghcr.io).

## Usage

### Build Docker Images Locally

For **Ubuntu**:
```bash
docker build -f Dockerfile-ubuntu-ci -t aequilibrae-ci-ubuntu:latest .
```

For **Windows**:
```powershell
docker build -f Dockerfile-windows-ci -t aequilibrae-ci-windows:latest .
```
