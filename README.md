# n8n with PostgreSQL - Docker Setup

This repository contains a Docker Compose configuration for running [n8n](https://n8n.io/) (a workflow automation tool) with PostgreSQL as the database backend.

## Overview

This setup includes:
- **n8n**: Latest version of n8n workflow automation platform
- **PostgreSQL 17**: Database for persisting n8n workflows and execution data

## Prerequisites

- Docker
- Docker Compose

## Configuration

The setup is configured with the following key settings:

### n8n Configuration
- **Port**: 5678
- **Protocol**: HTTP
- **Host**: 192.168.3.169
- **Basic Authentication**: Enabled
- **Runners**: Enabled

### PostgreSQL Configuration
- **Version**: PostgreSQL 17
- **Port**: 2131 (mapped from container port 5432)
- **Database**: n8n

### Default Credentials

> ⚠️ **Security Warning**: These are default credentials and should be changed for production use!

**n8n Basic Auth:**
- Username: `root`
- Password: `toor`

**PostgreSQL:**
- Username: `postgres`
- Password: `toor`
- Database: `n8n`

**Encryption Key:**
- Key: `krusty-krab`

## Usage

### Starting the Services

```bash
docker-compose up -d
```

This will start both n8n and PostgreSQL containers in detached mode.

### Stopping the Services

```bash
docker-compose down
```

### Viewing Logs

```bash
# View all logs
docker-compose logs -f

# View n8n logs only
docker-compose logs -f n8n

# View PostgreSQL logs only
docker-compose logs -f postgres
```

## Data Persistence

Data is persisted using Docker volumes:

- **n8n data**: `./n8n-data` - Contains n8n workflows, credentials, and settings
- **PostgreSQL data**: `./postgres-data` - Contains the PostgreSQL database files

## Accessing n8n

Once the containers are running, you can access n8n at:

```
http://192.168.3.169:5678
```

You will be prompted for basic authentication using the credentials mentioned above.

## Customization

To customize the configuration, edit the `docker-compose.yml` file and modify the environment variables as needed. Common changes include:

- Database credentials
- n8n host and port
- Encryption key
- Network settings

After making changes, restart the services:

```bash
docker-compose down
docker-compose up -d
```

## Network Mode

The n8n service is configured to use `host` network mode, which means it shares the host's network stack. This allows n8n to directly access services running on the host machine.
