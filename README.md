# Zabbix Deployment via Docker Compose

A production-ready stack for deploying Zabbix in Docker containers with strict separation of secrets and persistent data. Suitable for isolated network environments.

## Architecture

The `docker-compose.yml` includes the following core services:
* **zabbix-web** — Zabbix web interface (Nginx).
* **zabbix-server** — Main Zabbix server component.
* **zabbix-db** — PostgreSQL database securely isolated within the Docker network.
* **zabbix-agent** — Local Zabbix agent for host monitoring.

## Deployment Preparation

1. Clone the repository into a working directory on the server:
   ```bash
   git clone [https://github.com/malikovai/zabbix_docker_stack.git](https://github.com/malikovai/zabbix_docker_stack.git) .

2. Create the environment configuration file .env based on the provided template:
   ```bash
   cp .env.example .env
3. Edit .env to specify secure credentials and required environment variables (e.g., database passwords and proxy settings).

## Running the Stack

Deploy and start the containers in the background:
   ```bash
   docker compose up -d

## Maintenance and Backups

All stack data is persistent and isolated from Docker configuration files via local host volume mounts (./zabbix/db_data and ./zabbix_agent_conf). To perform a safe backup, stop the stack gracefully and backup the designated data directories:
   ```bash
   docker compose down
   # Perform backup of local data folders
   docker compose up -d

## Security Posture

Persistent data directories and the local secrets file (.env) are explicitly declared in .gitignore to prevent accidental commits. All sensitive data is injected exclusively via environment variables.
