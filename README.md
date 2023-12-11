# Elasticsearch-Kibana Docker Boilerplate

## Overview

This boilerplate provides a configuration for running Elasticsearch and Kibana in Docker containers. It's based on the official Docker Compose setup from Elastic, but with custom, opinionated enhancements for greater flexibility and control.

## Features

- **Single-node Elasticsearch**: Streamlined for a single node setup, making it simpler for development and testing environments.
- **Default Elasticsearch Version**: The Elasticsearch version is set to `8.11.2` by default, which can be updated as needed using the `ELASTIC_STACK_VERSION` environment variable.
- **Enhanced Environment Variable Management**: Advanced handling of environment variables like `ELASTIC_PASSWORD` and `KIBANA_SYSTEM_PASSWORD`, with error checks and default values.
- **Quick Security Toggle**: Easily toggle Elasticsearch security features on or off using the `ELASTIC_SECURITY_ENABLED` environment variable.
- **Elasticsearch Plugin Management**: Automated script to manage Elasticsearch plugins based on environment variables.
- **Dedicated Volume for Elasticsearch Plugins**: A dedicated volume for Elasticsearch plugins, allowing for persistent plugin management.
- **Robust Health Checks**: Improved health checks in services, taking into account the security settings.
- **Reliable Restart Policies**: Services are configured to restart unless explicitly stopped, enhancing uptime and reliability.
- **Default Reindex Remote Host**: The default allowed remote host for reindexing is set 172.17.0.1:*, the default IP address of the host system in Docker. This allows you to easily reindex from the host system (or a remote host using port forwarding).
- **Additional `app` Service**: A template for integrating a Python application that interacts with Elasticsearch and Kibana, including a Dockerfile (Python version 3.10.8).

## Getting Started

1. **Set Environment Variables**: Copy `.env.example` to `.env` and set the required variables.
2. **Docker Compose Up**: Run `docker-compose up` to start the services.
3. **Access Kibana**: Once the services are up, access Kibana at `http://localhost:${KIBANA_PORT}`.

## Customisation

- **Elasticsearch Plugins**: Adjust `ELASTIC_PLUGINS` in the `.env` file to manage plugins.
- **Toggle Security**: Set `ELASTIC_SECURITY_ENABLED` in `.env` to enable or disable Elasticsearch security features.

## Troubleshooting

### Elasticsearch fails to start using Docker: Max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]

You need to increase the value of vm.max_map_count with `sysctl -w vm.max_map_count=262144`.

On Windows, if you are using WSL (which should be the case with Docker Desktop), you can run `wsl -d docker-desktop`, followed by `sysctl -w vm.max_map_count=262144`.

To persist this change, you can add `vm.max_map_count = 262144` to `/etc/sysctl.conf` in WSL. I.e. for Docker Desktop on Windows with a WSL backend, you can run `wsl -d docker-desktop --exec sh -c "echo 'vm.max_map_count = 262144' >> /etc/sysctl.conf"` to persist this setting. See https://stackoverflow.com/a/66547784/1334688.

Try this fix even if you cannot locate the error message above - it may be burried somewhere in the logs.