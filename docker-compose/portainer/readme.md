# Portainer

# Required Files & Folder structure
```
.
├── docker-compose.override.yml
├── docker-compose.yml
└── portainer-data
```
`portainer-data` needs to be created

# Docker-compose.yml

Using docker-compose.override.yml to get traefik & watchtower configurations

## Volumes
```docker
    volumes:
      - /etc/localtime:/etc/localtime:ro # Passthrough host system time as read-only
      - /var/run/docker.sock:/var/run/docker.sock:ro #passthrough docker access as read-only
      - /PathTo/portainer/portainer-data:/data #mount local portainer data to container data-folder
```
## Network
```
    networks:
      - Proxy #Traefik network
```
## Docs
https://docs.portainer.io/