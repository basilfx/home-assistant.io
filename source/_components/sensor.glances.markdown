---
layout: page
title: "Glances"
description: "Instructions how to integrate Glances sensors into Home Assistant."
date: 2015-09-14 19:10
sidebar: true
comments: false
sharing: true
footer: true
logo: glances.png
ha_category: Sensor
ha_iot_class: "Local Polling"
---


The `glances` sensor platform is consuming the system information provided by the [Glances](https://github.com/nicolargo/glances) API. This enables one to track remote host and display their stats in Home Assistant.

This sensors needs a running instance of `glances` on the host. The minimal supported version of `glances` is 2.3:

```bash
glances -w
Glances web server started on http://0.0.0.0:61208/
```

Check if you are able to access the API located at `http://IP_ADRRESS:61208/api/2`. The details about your memory usage is provided as a JSON response. If so, you are good to proceed.

```bash
$ curl -X GET http://IP_ADDRESS:61208/api/2/mem/free
{"free": 203943936}
```

To enable the glances sensor, add the following lines to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
sensor:
  platform: glances
  name: Glances sensor
  host: IP_ADDRESS
  port: 61208
  resources:
    - 'disk_use_percent'
    - 'disk_use'
    - 'disk_free'
    - 'memory_use_percent'
    - 'memory_use'
    - 'memory_free'
    - 'swap_use_percent'
    - 'swap_use'
    - 'swap_free'
    - 'processor_load'
    - 'process_running'
    - 'process_total'
    - 'process_thread'
    - 'process_sleeping'
```

Configuration variables:

- **host** (*Required*): The IP address of your host, eg. 192.168.1.32.
- **port** (*Option*): The network port to connect to. Default is 61208.
- **name** (*Optional*): Name of the Glances sensor.
- **resources** (*Required*): Entries to monitor.
  - **'disk_use_percent'**: Used disk space in percent
  - **'disk_use'**: Used disk space
  - **'disk_free'**: Free disk space
  - **'memory_use_percent'**: Used memory in percent
  - **'memory_use'**: Used memory
  - **'memory_free'**: Free memory
  - **'swap_use_percent'**: Used swap space in percent
  - **'swap_use'**: Used swap space
  - **'swap_free'**: Free swap space
  - **'processor_load'**: Load
  - **'process_running'**: Number of running processes
  - **'process_total'**: Total number of processes
  - **'process_thread'**: Number of threads
  - **'process_sleeping'**: Number of sleeping processes

