# Exporter monitor cisco 3650
This project is built with:

- Python 3.6.x

And is packaged as a Docker container. The two top level dependencies are:

- prometheus
- netmiko
- psutil
- prometheus-client==0.0.21

See the [requirements file](./requirements.txt) for more details.

## Prometheus

monitoring application.

To instrument our Python code we need to manipulate the metrics each
time a new HTTP request is received.

See [the application](./app.py) for more details.

## Building

This project is automatically built by Docker Automated Builds.

To build manually:

`docker build -t cisco3650-exporter/tainguyenbp:v1.1 .`

## Running

Simply open port 9250 when running as a container:

`docker-comose up --build -d`

## Access URL check metrics

access url with port 9250:

`curl http://127.0.0.1:9250/metrics`

## Add config to the prometheus.yml file:

```
  - job_name: 'cisco3650_exporter'
    scrape_interval: 30s
    scrape_timeout: 30s
    static_configs:
    - targets: ['192.168.1.10:9250']
```

