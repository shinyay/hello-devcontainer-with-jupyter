# Hello Dev Container with Jupyter

I know that many Python developers use **Jupyter**. I have just started learning Python, but I use Jupyter to check the operation because it is useful.

The sample in this repository is a sample of running Jupyter in a Docker container and accessing and using that environment from VS Code.

## Description

There are three files used to configure this environment.

- **Dockerfile**
- **compose.yaml**
- **devcontainer.json**

Place them under the `.devcontainer` directory.

```shell
.devcontainer/
├── Dockerfile
├── compose.yaml
└── devcontainer.json
```

### .devcontainer directory

If there is a directory named `.devcontainer` in the `workspaceRoot`, VSCode's **RemoteDevelopment** extension will use the `.devcontainer.json` and other container-related files inside the directory for It does `docker build`, container creation, etc.

#### Dockerfile

```Dockerfile
FROM python:3.12.1-slim-bullseye
USER root

RUN apt-get update && \
    apt-get -y install --reinstall ca-certificates && \
    apt-get -y install software-properties-common && \
    pip install --upgrade pip

RUN pip install ipykernel jupyter
```

- `L1`: A container image of the latest Python version as of Jan-11-2024 is specified.
- `L4-L7`: I have installed the minimum required packages and upgraded `pip` to provide a base Python environment.
- `L9`: Two modules required for **Jupyter** are installed.

#### compose.yaml

```yaml
version: "3"
services:
  jupyter:
    build:
      context: ..
      dockerfile: .devcontainer/Dockerfile
    environment:
      PYTHONPATH: /workspace
    volumes:
      - ..:/workspace
    ports:
      - 8888:8888
    command: sleep infinity
```

- `L6`: Specify the PATH of Dockerfile
- `L10`: Define the path of the workspace on the container

#### devcontainer.json

```json
{
	"name": "devcontainr_python3",
	"dockerComposeFile": "compose.yaml",
	"service": "jupyter",
	"workspaceFolder": "/workspace",
	"shutdownAction": "stopCompose",
	"forwardPorts": [8888],
	"customizations": {
		"vscode": {
			"extensions": [
                "ms-python.python",
				"ms-python.vscode-pylance",
                "ms-toolsai.jupyter"
            ]
		}
	}
}
```

- `L2`: Container name visible on VS Code
- `L3`: Specify by relative path the docker-comopse file used to create the container
- `L4`: Specify the service name of the container you want to open in VScode among the services in compose.yaml
- `L5`: Specify the root folder when the container is opened
- `L6`: Setting what to do with containers when a container screen is closed in VScode. `stopCompose` stops the container when the screen is closed
- `L11-L13`: Specify VScode extensions to be installed with container creation
  - [ms-python.python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
  - [ms-python.vscode-pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)
  - [ms-toolsai.jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)

### Execute Dev Containers

Follow the steps below to execute **Dev Containers**.

1. Open **Command Pallette** by `F1`
2. Select `> Dev Containers: Reopen in Container`
3. Open **Command Pallette** by `F1` on the Remote side 
4. Select `> Jupyter: Import Jupyter Notebook`
5. Select `Interactive-1.ipynb`
6. Select `Run Cell`

## Demo

## Features

- feature:1
- feature:2

## Requirement

## Usage

## Installation

## References

## Licence

Released under the [MIT license](https://gist.githubusercontent.com/shinyay/56e54ee4c0e22db8211e05e70a63247e/raw/34c6fdd50d54aa8e23560c296424aeb61599aa71/LICENSE)

## Author

- github: <https://github.com/shinyay>
- twitter: <https://twitter.com/yanashin18618>
- mastodon: <https://mastodon.social/@yanashin>
