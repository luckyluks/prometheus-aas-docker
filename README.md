# Prometheus-AAS-Docker

Move device metric data into the AAS using the [Prometheus-AAS-Router](https://github.com/n14s/prometheus-aas-router) within a dockerized Prometheus-AAS stack.

## Goal

This repo demonstrates a minimal Docker Compose setup, sending a machines metrics, recorded by [Prometheus](https://prometheus.io/), into the [Asset Administation Shell](https://www.plattform-i40.de/IP/Redaktion/EN/Standardartikel/specification-administrationshell.html), the Digital Twin Solution for Industry 4.0, using the [Prometheus-AAS-Router](https://github.com/n14s/prometheus-aas-router)

## Docker Compose

This Docker Compose stack includes the following services:

- [Prometheus](https://github.com/prometheus/prometheus)
- [Node-Exporter](https://github.com/prometheus/node_exporter)
- [Cadvisor](https://github.com/google/cadvisor)
- [Prometheus-AAS-Router](https://github.com/luckyluks/prometheus-aas-router)

## Setup

1. pull the repo and include the submodules
    ```console
    git clone --recurse-submodules https://github.com/luckyluks/prometheus-aas-docker.git
    ```

2. change in repo
    ```console
    cd prometheus-aas-docker/
    ```

3. adapt the ``.env`` file
    ```console
    nano .env
    ```
    Things to change:
    - REGISTRY_HOST_FQDN: the fqdn of the registry host. For local development you can use a [local registry (see below)](#local-registry)
    - HOSTNAME_FQDN: the fqdn hostname of the host you want to start the stack. For local development you can use `localhost`
    - ASSET_ID: arbitrary ID (e.g. UUID) which is used to identify the host in the registry

4. pull the repo and include the submodules
    ```console
    docker-compose up -d --build
    ```
5. check if node is registered, e.g. with: 
    ```console
    source .env && curl -q http://$REGISTRY_HOST_FQDN:4000/registry/api/v1/registry | grep $ASSET_ID
    ```


## Take down gracefully

in order to take down the stack and deregister AAS at registery, use:
```console
docker-compose down -v
```
## Configuration

The config dir contains folders with config files of the individual services.  
Those config-folders are mounted onto the container.  
The config files in this repo contain a example setup, pushing elemental device metrics into the AAS.  
Further information on how to configure the individual services can be found on their respective websites.


## Local registry

In order to register the provided AAS in a registry, a local version can be brought up with
```console
docker-compose -f registry.yml up -d
```
In this case the environment variable `REGISTRY_HOST_FQDN` and `HOSTNAME_FQDN` can be assigned as following in the `.env` file: 
```console
REGISTRY_HOST_FQDN=host.docker.internal
HOSTNAME_FQDN=localhost
ASSET_ID=someRandomId
```