FROM python:3.12.1-slim-bullseye
USER root

RUN apt-get update && \
    apt-get -y install --reinstall ca-certificates && \
    apt-get -y install software-properties-common && \
    pip install --upgrade pip

# Install Basic Packages
RUN pip install ipykernel jupyter