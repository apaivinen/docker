# Traefik

Reverse proxy for web services

> **Note**
> Create a new docker network before running docker compose the first time.  
> `docker network create Proxy`  
> This needs to be only once. You need to attach serveces to this network if you want Traefik to handle routing

Don't forget to add DNS entries to Pi-Hole.

If you need to access traefik container content use `docker exec -it traefik ash`

# ToDo
Update config.yml for static routing configuration. Currenlty there's empty template file.


---


## Required File & Folder structure
```
.
├── data
│   ├── config.yml
│   ├── logs
│   │   ├── access.log
│   │   └── traefik.log
│   ├── ssl
│   │   └── acme.json
│   └── traefik.yml
├── docker-compose.yml
└── traefik.env
```

you must provide `config.yml` content  

`traefik.log` is automatically generated if logging is turned on  
`access.log` is automatically generated if accessLog is turned on  

`acme.json` is automatically created when you start start the container  

you must provide `traefik.yml` content  



# docker-compose.yml
## Volumes

```docker
    volumes:
      - /etc/localtime:/etc/localtime:ro # Passtrhough local system time config as read only
      - /var/run/docker.sock:/var/run/docker.sock # Mandatory
      - /Path/To/traefik/data/traefik.yml:/etc/traefik/traefik.yml:ro # Custom configs location
      - /Path/To/traefik/data/config.yml:/etc/traefik/config.yml:ro # Custom configs location
      - /Path/To/traefik/data/ssl:/etc/traefik/ssl # Custom certificate location
      - /Path/To/traefik/data/logs:/var/log # Custom log location
```
## Networks

Add container to Proxy network
```docker
    networks:
      - Proxy
```

## Environment variables
I'm passing cloudflare credentials from environment file
```docker
    env_file:
      - /path/to/traefik/traefik.env # Load cloudflare auth info
```

## Usage

## Docs

Traefik docs basic compose example: https://doc.traefik.io/traefik/user-guides/docker-compose/basic-example/  
Traefik docs examples: https://doc.traefik.io/traefik/v1.7/user-guide/examples/  
Traefik examples: https://github.com/DoTheEvo/  Traefik-v2-examples#2-traefik-routing-to-a-local-IP-addresses  
Christian lempa traefik yml: https://github.com/ChristianLempa/boilerplates/blob/main/docker-compose/traefik/config/traefik.yml  
Technotim blog post: https://docs.technotim.live/posts/traefik-portainer-ssl/  
Technotim video: https://www.youtube.com/watch?v=liV3c9m_OX8  