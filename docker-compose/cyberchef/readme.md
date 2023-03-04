# Cyberchef container

This is the same container as [here](https://github.com/apaivinen/docker/tree/main/dockerfile/cyberchef) but with my environment settings. 

1. Copy files to CyberChef folder on your docker machine
2. Navigate to your CyberChef folder and run `docker compose up -d` to build an image
3. Browse to http://127.0.0.1:80 to access CyberChef (or url defined in traefik configurations)

File structure should be following:
```
├── docker-compose.override.yml
├── docker-compose.yml
├── Dockerfile
└── README.md
```
`docker-compose.yml` contains container build & run configurations
`docker-compose.override.yml` contains traefik configurations
`Dockerfile` is a which CyberChef image is based on

Don't forget to change `cyberchef.local.yourDomain.com` in `docker-compose.override.yml` to match your configurations

# Container (dockerfile) explanation
Build process is divided to two parts
    1. build
    2. main

## Build

- Uses nginx:1.23.3-alpine-slim image as base image
- Installs necessary packages to clone & compile Cyberchef from github
- unzips compiled files to nginx default directory `/usr/share/nginx/html/`
- sets CyberChef-VERSIONNUMBER.html to index.html

## Main

- Copies `/usr/share/nginx/html/` files from build to main
- Runs nginx server

