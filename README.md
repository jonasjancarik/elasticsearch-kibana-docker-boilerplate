# Elasticsearch & Kibana Docker Boilerplate

## Overview

This boilerplate provides a configuration for running Elasticsearch and Kibana in Docker containers. It's based on the [official Docker Compose file](https://github.com/elastic/elasticsearch/blob/8.11/docs/reference/setup/install/docker/docker-compose.yml) from Elastic, but with custom enhancements for greater flexibility and control. Additionally, it includes a separate Docker Compose setup for a custom application that interacts with Elasticsearch and Kibana.

## Features

- **Single-node Elasticsearch Setup**: Configured for a single-node (es01) setup, suitable for development and testing environments.
- **Default Elasticsearch Version**: Sets the Elasticsearch version to `8.11.2` by default, adjustable via the `ELASTIC_STACK_VERSION` environment variable.
- **Security Toggle**: Provides the option to enable or disable Elasticsearch security features using the `ELASTIC_SECURITY_ENABLED` environment variable; Kibana is automatically configured to adapt to the security configuration and healthcheks are adjusted accordingly.
- **Elasticsearch Plugin Script**: Includes a script to automate the management of Elasticsearch plugins, driven by environment variables.
- **Volume for Elasticsearch Plugins**: Allocates a specific volume for Elasticsearch plugins to speed up container startup.
- **Restart Policy**: Configures services to automatically restart unless they are explicitly stopped, making it easier to keep the stack running.
- **Separate Compose File for Custom App**: Utilizes a separate Docker Compose file (`docker-compose-app.yml`) for the integration of a custom application, enabling independent management.

## Getting Started

### Running Elasticsearch and Kibana

First, ensure that vm.max_map_count is set to at least 262144. 

1. **Ensure correct vm.max_map_count**: See https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#_set_vm_max_map_count_to_at_least_262144
2. **Set Environment Variables**: Copy `.env.example` to `.env` and set the required variables.
3. **Start Services**: Run `docker-compose up` to start the Elasticsearch and Kibana services.
4. **Access Kibana**: Once the services are up, access Kibana at `http://localhost:${KIBANA_PORT}`.

### Running with Custom App

To run the Elasticsearch stack along with a custom application:

1. **Set Up the Elasticsearch Stack**: Follow the steps above to set up the environment variables and start the Elasticsearch and Kibana services.
2. **Start All Services Including the App**: Run `docker-compose -f docker-compose.yml -f docker-compose-app.yml up` to start all services, including the custom application.

## Customisation

- **Elasticsearch Plugins**: Adjust `ELASTIC_PLUGINS` in the `.env` file to manage plugins.
- **Security Toggle**: Use `ELASTIC_SECURITY_ENABLED` in `.env` to enable or disable Elasticsearch security features.
