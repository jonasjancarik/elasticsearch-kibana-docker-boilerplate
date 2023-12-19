# Elasticsearch & Kibana Docker Boilerplate

## Overview

This boilerplate provides a configuration for running Elasticsearch and Kibana in Docker containers. It's based on the [official Docker Compose file](https://github.com/elastic/elasticsearch/blob/8.11/docs/reference/setup/install/docker/docker-compose.yml) from Elastic, but with custom enhancements for greater flexibility and control. Additionally, it includes a separate Docker Compose setup for a custom application that interacts with Elasticsearch and Kibana.

## Features

- **Single-node Elasticsearch setup**: Configured for a single-node (es01) setup, suitable for development and testing environments.
- **Default Elasticsearch version**: Sets the Elasticsearch version to `8.11.2` by default, adjustable via the `ELASTIC_STACK_VERSION` environment variable.
- **Security toggle**: Provides the option to enable or disable Elasticsearch security features using the `ELASTIC_SECURITY_ENABLED` environment variable; Kibana is automatically configured to adapt to the security configuration and healthcheks are adjusted accordingly.
- **Elasticsearch plugin script**: Includes a script to automate the management of Elasticsearch plugins, driven by environment variables.
- **Volume for Elasticsearch plugins**: Allocates a specific volume for Elasticsearch plugins to speed up container startup.
- **Restart policy**: Use the `RESTART_POLICY` environment variable to configure the [restart policy](https://docs.docker.com/config/containers/start-containers-automatically/) for Elasticsearch and Kibana containers centrally. The default is set to `no`.
- **Separate Docker Compose file for a custom Python app**: Quickly set up a Python app as part of the stack interact using the `docker-compose-app.yml`). The app should be set up in the same directory as the Docker files.

## Getting Started

### Running Elasticsearch and Kibana

First, ensure that vm.max_map_count is set to at least 262144. 

1. **Ensure correct vm.max_map_count**: See https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#_set_vm_max_map_count_to_at_least_262144
2. **Set Environment Variables**: Copy `.env.example` to `.env` and set the required variables.
3. **Start Services**: Run `docker compose up` to start the Elasticsearch and Kibana services (or `docker compose up -d` to run in detached mode in the background).
4. **Access Kibana**: Once the services are up, access Kibana at `http://localhost:${KIBANA_PORT}`.

### Running with Custom App

To run the Elasticsearch stack along with a custom application:

1. **Set up your app**: Set up your Python app in the same directory as the Docker files. Make sure a requirements.txt file is present, even if empty.
2. **Set Up the Elasticsearch Stack**: Follow the steps above to set up the environment variables and start the Elasticsearch and Kibana services.
3. **Start All Services Including the App**: Run `docker compose -f docker-compose.yml -f docker-compose-app.yml up` to start all services, including the custom application.

The app will have access to the same Docker network, so the service names (`es01` and `kibana`) should be used as host names, not `localhost`.

## Customization

- **Elasticsearch Plugins**: Adjust `ELASTIC_PLUGINS` in the `.env` file to manage plugins.
- **Security Toggle**: Use `ELASTIC_SECURITY_ENABLED` in `.env` to enable or disable Elasticsearch security features.
