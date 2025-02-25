# ExifTool CLI Docker Container
[![Create and publish a Docker image](https://github.com/GewoonJaap/exiftool-docker/actions/workflows/publish.yml/badge.svg)](https://github.com/GewoonJaap/exiftool-docker/actions/workflows/publish.yml)

This repository provides a Docker container for the ExifTool CLI, allowing you to interact with the ExifTool CLI without installing it on your machine.

## Prerequisites

- Docker installed on your machine.

## Building the Docker Image (OPTIONAL)

To build the Docker image, run the following command:

```sh
docker build --build-arg TARGETARCH=$(uname -m) -t exiftool-docker:latest .
```

This command will build the Docker image for the appropriate architecture (amd64, arm, or arm64).

## Running the exiftool
```sh
docker run -v $(pwd):/data -w /data ghcr.io/gewoonjaap/exiftool-docker:latest FILENAME
```

## Aliasing the docker command
You can alias the docker command to be able to run exiftool directly in your terminal. Add the following to your `.bashrc`
```sh
alias exiftool='docker run -v $(pwd):/data -w /data ghcr.io/gewoonjaap/exiftool-docker:latest $1'
```

Then you can use the following in your terminal, which will run the command in the docker container
```sh
exiftool FILENAME
```

## Opening the docker container
- Run the docker container with the following command:
```sh
docker run -it -v <MEDIALOCATION>:/data ghcr.io/gewoonjaap/exiftool-docker:latest /bin/bash
```

This command will run the ExifTool CLI in the Docker container and mount the desired directory to the `/data` directory in the container.
Now attach a console to the Docker container and run the ExifTool CLI commands as you would on your local machine.

### Example command
You can replace `/data` with any other direction you want.
The `exiftool` executable is available in the container, in the exiftool/ folder, so you can run any ExifTool CLI command you would like.
```sh
cd exiftool
./exiftool "-FileCreateDate<FileCreateDate" "-FileModifyDate<FileCreateDate" -ext .mp4 -ext .jpg -ext .jpeg -ext .heic -ext .MOV -ext .png /data
```

```sh
cd exiftool
./exiftool "-FileCreateDate<CreateDate" "-FileModifyDate<CreateDate" -ext .mp4 -ext .jpg -ext .jpeg -ext .heic -ext .MOV -ext .png /data
```
