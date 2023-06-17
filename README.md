# linuxserver-io-mod-swag-env-auto-config

A linuxsever/swag mod that automatically enables select proxy configs based on environment variables.

# Usage
- Append `ghcr.io/jubast/linuxserver-io-mod-swag-env-auto-config` to the `DOCKER_MODS` environment variable.
- The script will be run everytime the container is restarted.

# Supported proxy configs (more will be added when needed)
- Homeassistant
- Nextcloud

# Supported Enviroment variables (more will be added when needed)
- AUTO_HOMEASSISTANT=true
- AUTO_NEXTCLOUD=true
- AUTO_NEXTCLOUD_HSTS=true # add the HSTS header in the nextcloud.subdomain.conf
- AUTO_NEXTCLOUD_NO_ROBOTS=true # add the X-Robots-Tag header in the nextcloud.subdomain.conf

Example:
```yml
version: "3.2"
services:
  swag:
    image: lscr.io/linuxserver/swag:latest
    container_name: swag
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Ljubljana
      ...
      - AUTO_HOMEASSISTANT=true
      - AUTO_NEXTCLOUD=true
      - AUTO_NEXTCLOUD_HSTS=true
      - AUTO_NEXTCLOUD_NO_ROBOTS=true
      - DOCKER_MODS=ghcr.io/jubast/linuxserver-io-mod-swag-env-auto-config
    volumes:
      - config:/config
    ports:
      - 443:443
    networks:
      - public
    restart: unless-stopped

volumes:
  config:


networks:
  public:
    driver: bridge

```
