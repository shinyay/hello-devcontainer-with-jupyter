# Hello Dev Container with Jupyter

I know that many Python developers use **Jupyter**. I have just started learning Python, but I use Jupyter to check the operation because it is useful.

## Description

### Directory

The project consists of the following

```shell
.devcontainer/
├── Dockerfile
├── compose.yaml
└── devcontainer.json
```

```Dockerfile
FROM python:3.12.1-slim-bullseye
USER root

RUN apt-get update && \
    apt-get -y install --reinstall ca-certificates && \
    apt-get -y install software-properties-common && \
    pip install --upgrade pip

# Install Basic Packages
RUN pip install ipykernel jupyter
```

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

```json
{
	"name": "devcontainr_python3",
	//"dockerFile": "Dockerfile",
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
            ],
			"settings": {
				"python.defaultInterpreterPath": "/usr/local/bin/python3",
                "workbench.colorCustomizations": {
                    "titleBar.activeBackground": "#19549C",
                    "titleBar.activeForeground": "#ffffff",
                    "activityBar.background": "#02A7E3",
                    "activityBar.foreground": "#ffffff"
                }
            }
		}
	}
}
```

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
