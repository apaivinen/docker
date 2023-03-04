# Bitwarden

Installation is done by following deploy guide from here https://github.com/bitwarden/server

I'm using Traefik to provide reverse proxy & secure connection. Traefik settings are stored in `docker-compose.override.yml` file so the configurations won't be wiped when docker-compose updates.

I'm using gmail account to send out bitwarden notifications. Follow gmail instructions how to [create app password](https://support.google.com/accounts/answer/185833?hl=en).

## Installation

```bash
mkdir /PathToYourLocation/bitwarden
cd /PathToYourLocation/bitwarden
```
```bash
curl -s -L -o bitwarden.sh \
    "https://func.bitwarden.com/api/dl/?app=self-host&platform=linux" \
    && chmod +x bitwarden.sh
./bitwarden.sh install
```
### Installation questions
1. Enter the domain name for your Bitwarden Instance: Full domain name (ex. bitwarden.local.yourdomain.com)  
2. Do you want to use let's encrypt to generate a free SSL certificate? No since I'm using Traefik with certificate  
3. Enter the database name for your bitwarden instance... Pick your name.  
4. Enter your installation ID: Get the ID from the link provided or use your existing one  
5. Enter installation key: Get the ID from the link provided or use your existing one  
6. Do you have a SSL certificate to use? No
7. Do you want to generate a self-signed SSL certificate? yes

Done.

## Configuration

1. Add `docker-compose.override.yml` to `/PathToYourLocation/bitwarden/bwdata/docker/docker-compose.override.yml`
2. Configure `/PathToYourLocation/bitwarden/bwdata/env/global.override.env` atleast following properties
   - globalSettings__mail__replyToEmail=no-reply@yourdomain
   - globalSettings__mail__smtp__host=smtp.gmail.com
   - globalSettings__mail__smtp__port=587
   - globalSettings__mail__smtp__ssl=true
   - globalSettings__mail__smtp__username=validGmailAccount
   - globalSettings__mail__smtp__password=ValidGmailAccountAppPassword
   - adminSettings__admins=yourEmailWhichYouUseForLogin
3. From `/PathToYourLocation/bitwarden/bwdata/config.yml` modify values as following
   - ssl: false
   - ssl_managed_lets_encrypt: false
### Optional

Comment port settings from file `/PathToYourLocation/bitwarden/bwdata/docker/docker-compose.yml` from service `nginx` since there's no need to expose them. Keep in mind theese will be uncommented when docker-compose is updated. If you want to manually manage docker-compose file you can set `generate_compose_config: true` to `false` from `../bwdata/config.json`
## Start the bitwarden instance
Run following commands to update configurations & start bitwarden
```
/PathToYourLocation/bitwarden/bitwarden.sh updateself
/PathToYourLocation/bitwarden/bitwarden.sh update
/PathToYourLocation/bitwarden/bitwarden.sh start
```
# Cheathseet for updating configs
```bash
./bitwarden.sh stop
./bitwarden.sh updateself
./bitwarden.sh update
./bitwarden.sh start 
```
# Sources
- Great introduction from Lawrence systems [How to Setup Self Hosted Bitwarden](https://youtu.be/SSLGa0LjTrA)
- Label example copied from vaultwarden [Proxy Examples](https://github.com/dani-garcia/vaultwarden/wiki/Proxy-examples)
- [Bitwarden Github](https://github.com/bitwarden/server)
- [Bitwarden Docs](https://bitwarden.com/help/)
- If your paranoia is too strong about PBKDF2 iterations then check this [1password post](https://blog.1password.com/1password-hashcat-strong-master-passwords/)
   - Bitwarden community [blog post](https://community.bitwarden.com/t/increasing-the-default-number-of-pbkdf2-for-existing-accounts/49550)
   - Bitwarden [Mastodon post](https://fosstodon.org/@bitwarden/109745277062224768)
- Fun fact, [password strenght tool](https://bitwarden.com/password-strength/) from Bitwarden