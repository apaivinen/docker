docker build -t apa/evilgnix2 .
https://github.com/vishnudxb/docker-evilginx2

https://github.com/froyo75/docker-evilginx2/tree/main

https://github.com/warhorse/docker-evilginx2

```docker
docker create --name=evilginx2 -e TZ=Europe/London -p 445:443 -p 85:80 -v ./config:/config -v ./phislets:/phishlets --restart unless-stopped apa/evilgnix2:latest

```



lataa phisletit `/app# evilginx -p phishlets/`