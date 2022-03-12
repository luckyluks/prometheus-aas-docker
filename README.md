# Prometheus-AAS-Docker

Move device metric data into the AAS using the [Prometheus-AAS-Router](https://github.com/n14s/prometheus-aas-router) within a dockerized Prometheus-AAS stack.

## Goal

This repo demonstrates a minimal Docker Compose setup, sending a machines metrics, recorded by [Prometheus](https://prometheus.io/), into the [Asset Administation Shell](https://www.plattform-i40.de/IP/Redaktion/EN/Standardartikel/specification-administrationshell.html), the Digital Twin Solution for Industry 4.0, using the [Prometheus-AAS-Router](https://github.com/n14s/prometheus-aas-router)

## Docker Compose

This Docker Compose stack includes the following services:

- [Prometheus](https://github.com/prometheus/prometheus)
- [Node-Exporter](https://github.com/prometheus/node_exporter)
- [AAS-Server](https://wiki.eclipse.org/BaSyx_/_Documentation_/_Components_/_AAS_Server)
- [Prometheus-AAS-Router](https://github.com/n14s/prometheus-aas-router)

Note: The prometheus image is slighty altered, only preparing its filesystem for a clean bind mount of its config files. The image is hosted on Docker Hub, its Dockerfiles can be inspected in the build directory.

To start the stack, simply run  
`docker-compose up`

## Configuration

The config dir contains folders with config files of the individual services.  
Those config-folders are mounted onto the container.  
The config files in this repo contain a example setup, pushing elemental device metrics into the AAS.  
Further information on how to configure the individual services can be found on their respective websites.
