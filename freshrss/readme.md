# FreshRSS

"FreshRSS is a self-hosted RSS and Atom feed aggregator."

This compose file contains traefik network & labels

## Required File & Folder structure
```
.
├── configs.env
├── data
├── docker-compose.yml
└── extensions
```
`configs.env` is not in use currently  
`data` folder will be populated by the container  
`extensions` folder will be populated by the container  

# Docker-compose.yml

## Volumes

```
    volumes:
      - /Path/To/freshrss/data:/var/www/FreshRSS/data
      - /Path/To/freshrss/extensions:/var/www/FreshRSS/extensions
```

## Networks
```
    networks:
      - Proxy #Traefik network
```
## Environment variables

There's `configs-EXAMPLE.yml` which is not in use currently. Refer to FreshRSS documentation for more information.

```
    environment:
      TZ: Europe/Helsinki
      CRON_MIN: '3,33'
```
Just simple timezone & refresh cronjob values

## Docs
https://github.com/FreshRSS/FreshRSS/tree/edge/Docker  
https://github.com/FreshRSS/FreshRSS  
https://github.com/FreshRSS/Extensions  