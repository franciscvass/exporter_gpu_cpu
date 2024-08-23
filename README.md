# README

## supported OS Versions
- It was tested on Ubuntu 22.04 and Oracle Linux 8 with Nvidia drivers installed ([see here](https://docs.oracle.com/en-us/iaas/images/image/55a32890-2cfa-42d2-92d9-998a31eecfd0/))

## role dcgm-exporter

- it installs Nvidia DCGM and DCGM Exporter on Oracle Linux and Ubuntu
- it assume the Nvidia drivers are installed on Oracle Linux. For Ubuntu it installs Nvidia drivers 
- it uses Docker composer on Oracle Linux to manage the container that collects and exposes the metris
- it uses Docker on Ubuntu to manage the container that collects and exposes the metris
- the GPU metris are exposed on Host_IP:9400/metrics

## role node-exporter

- it uses Docker Composer to run a container that collects abd exposes metrics on Host_IP:9100/metrics

## How to run it

- Use __exporter.yaml__ to include both roles
- There are some vars you can override
- Use __inventory__ as an example for ansible inventory

```
ansible-playbook -i inventory exporter.yaml --private-key <parh to ssh private key>
```

## to test if metrics are published

- run the play-book test_exporters.yaml
- for each host you should see GPU metrics and node metrics
- In case of any errors start by checking the Docker container logs and then look into systemd logs (both container are managed by systemd)
