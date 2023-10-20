## Xray Docker Image by Teddysun

[Xray][1] is a platform for building proxies to bypass network restrictions.

It secures your network connections and thus protects your privacy.

Docker images are built for quick deployment in various computing cloud providers.

For more information on docker and containerization technologies, refer to [official document][2].

## Prepare the host

If you need to install docker by yourself, follow the [official installation guide][3].

## Pull the image

```bash
$ docker pull teddysun/xray
```

This pulls the latest release of Xray.

It can be found at [Docker Hub][4].

## Start a container

You **must create a configuration file**  `/etc/xray/config.json` in host at first:

```
$ mkdir -p /etc/xray
```

A sample in JSON like below:

```
{
  "inbounds": [{
    "port": 9000,
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "1eb6e917-774b-4a84-aff6-b058577c60a5",
          "level": 1,
          "alterId": 64
        }
      ]
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  }]
}
```

Or generate a configuration file online by [https://tools.sprov.xyz/v2ray/](https://tools.sprov.xyz/v2ray/)

There is an example to start a container that listen on port `9000`, run as a Xray server like below:

```bash
$ docker run -d -p 9000:9000 --name xray --restart=always -v /etc/xray:/etc/xray teddysun/xray
```

**Warning**: The port number must be same as configuration and opened in firewall.

[1]: https://github.com/XTLS/Xray-core
[2]: https://docs.docker.com/
[3]: https://docs.docker.com/install/
[4]: https://hub.docker.com/r/teddysun/xray/

---

# On VPS:

```bash
# Generate cert by acme
# /root/cert.crt
# /root/private.key

# Install Docker
# https://docs.docker.com/engine/install/ubuntu/

# Clone source
git clone https://github.com/chiasetuyetvoi/across.git
cd across/docker/xray

# Edit path
vim Dockerfile
# Remove `./docker/xray/`

# Build image
docker build -t docker-xray .

# Create config
sudo mkdir -p /etc/xray
sudo vim /etc/xray/config.json
# https://github.com/XTLS/Xray-examples

# Run image
docker run -d -p 9000:9000 -p 80:80 -p 443:443 --name docker-xray --restart=always -v /etc/xray:/etc/xray docker-xray
```