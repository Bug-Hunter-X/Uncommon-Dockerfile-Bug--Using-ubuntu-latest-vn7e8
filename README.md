# Uncommon Dockerfile Bug: Using `ubuntu:latest`

This repository demonstrates a common but often overlooked issue in Dockerfiles: using the `ubuntu:latest` base image. While convenient, this practice can lead to unexpected build failures and inconsistencies in your Docker images due to the frequent updates to the `latest` tag.

## Bug
The original `Dockerfile` uses `ubuntu:latest`. This means that the image your Dockerfile produces will depend on the version of Ubuntu that is currently the `latest` tag, which can change at any time, breaking existing builds.

## Solution
The `DockerfileFixed` uses a specific version of Ubuntu, e.g., `ubuntu:22.04`. This guarantees that the image will use a consistent base image, making your builds reproducible and reliable.

## How to Reproduce
1. Clone this repository.
2. Build the original Dockerfile: `docker build -t ubuntu-latest -f Dockerfile .`
3. Build the fixed Dockerfile: `docker build -t ubuntu-2204 -f DockerfileFixed .`
4. Observe the different image IDs, indicating different base images.
5. If the `latest` tag changes in future, any new build from the original dockerfile will use the newer version. However, `ubuntu:22.04` will always remain the same.