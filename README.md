```markdown
# Portainer Docker Setup

A simple Docker Compose setup to run Portainer - a lightweight management UI for Docker environments.

## What is Portainer?

[Portainer](https://www.portainer.io/) is a web-based user interface that allows you to easily manage your Docker hosts, containers, images, volumes, and networks.

## Prerequisites

- Docker installed on your system
- Docker Compose installed on your system
- Ports 8000 and 9000 available on your host machine

## Quick Start

1. **Clone this repository**
   ```bash
   git clone https://github.com/AlirezaTaaty/docker-GUI.git
   cd docker-GUI
   ```

2. **Start Portainer**
   ```bash
   docker-compose up -d
   ```

3. **Access Portainer**
   - Open your web browser and go to: `http://localhost:9000`
   - Follow the initial setup wizard to create an admin user

## Port Configuration

- **Port 9000**: Web UI (HTTP)
- **Port 8000**: Portainer agent communication
- **Port 9443**: HTTPS (currently commented out in the configuration)

## Volumes

- `portainer_data`: Persistent storage for Portainer configuration data
- Docker socket: Allows Portainer to manage your Docker environment

## Security Notes

⚠️ **Important Security Considerations:**

- Mounting the Docker socket (`/var/run/docker.sock`) gives Portainer full control over your Docker daemon
- Consider using HTTPS in production (uncomment port 9443 and configure SSL)
- Expose these ports only on trusted networks
- Change the default ports if needed for your environment

## Management Commands

```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs -f

# Stop and remove with volumes (warning: deletes all data)
docker-compose down -v
```

## Data Persistence

Your Portainer data is persisted in the `portainer_data` volume. To backup your data:

```bash
# Backup volume
docker run --rm -v portainer_data:/source -v $(pwd):/backup alpine tar czf /backup/portainer_backup.tar.gz -C /source ./
```

## Troubleshooting

- If you can't access the UI, check if ports 8000 and 9000 are available
- Verify Docker daemon is running: `docker info`
- Check container status: `docker-compose ps`
