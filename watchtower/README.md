# Watchtower

Update specified container images automatically

## Required File & Folder structure
```
watchtower
├── data
│   └── config.json
├── docker-compose.yml
└── watchtower.env
```

config.json is required for this container to work. More information about usage in here https://containrrr.dev/watchtower/private-registries/#docker_config_path

# docker-compose.yml
## Volumes

Mount `/etc/timezone:/etc/timezone:ro`

Mount `/var/run/docker.sock:/var/run/docker.sock:ro`  
Currently testing if read only (:ro) is enough

Mount `/path/to/watchtower/data/config.json:/config.json`


## Environment variables
Add environment variables from file
```docker
 env_file:
      - /path/to/watchtower/watchtower.env
```

# Discord

Create webhook, get the url and parse token & channel id
Url should looke like this `https://discord.com/api/webhooks/webhookid/token`  
Parse url to format: `discord://token@webhookid`  
Add this to `WATCHTOWER_NOTIFICATION_URL` variable in `watchtower.env`


# Usage

Just add following label to containers you want to update automatically via watchtower  
`com.centurylinklabs.watchtower.enable=true`

Watchtower will automatically find every containers where the label is set to `true`

## Docs

Watchtower docs:
https://containrrr.dev/watchtower/usage-overview/  
Notification docs:
https://containrrr.dev/shoutrrr/v0.6/services/overview/  
Discord notifications https://containrrr.dev/shoutrrr/v0.6/services/discord/  