# Cyberchef container

This is selfmade container for practice.
Here's a link to [CyberChef repository](https://github.com/gchq/CyberChef)

1. Copy files to CyberChef folder on your docker machine
2. Navigate to your CyberChef folder and run `docker compose up -d` to build an image
3. Browse to http://127.0.0.1:80 to access CyberChef

File structure should be following:
```
├── docker-compose.yml
├── Dockerfile
└── README.md
```
`docker-compose.yml` contains build & run configurations  
`Dockerfile` is a build file for CyberChef container

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

