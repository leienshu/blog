---
title: "Install V2ray"
date: 2020-12-26T13:46:59+08:00
draft: false
description: "Just in case"
tags: [v2ray]
---
I can not write this in Chinese , but I really want to write it down .

## first 

please get an ECS or VPS which can visit the world outside of the wall.

* CentOS 7.x + 
* Debian
* Ubuntu 18.x +

i choose Cent OS 8.3, so the following content is based on Cent OS 8.

## second

download the installation script by this command.

```shell
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh
```
then you will get a file which named 'install-release.sh'

run this script.

```shell
bash install-release.sh
```

## third 

after the installation , we should do some configuration for v2ray.

* add the v2ray service to startup list 

```shell
systemctl enable v2ray
```

* start the v2ray service 

```shell
systemctl start v2ray
```

## fourth

at last , we should config our server and client.

unluckly , most people don't know how to set the configration file. Actually , there is no need to know too much about it , you just need to know how to copy and modify my code.

* for server

the config.json file is located in /usr/local/etc/v2ray/ here.

```json
{
  "log":{
        "loglevel":"warnning",
        "access":"/var/log/v2ray/access.log",
        "error":"/var/log/v2ray/error.log"
        },
  "inbounds": [
    {
      "port": 1027,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "39f91024-f331-46d8-90e5-4046a05bea77",
            "alterId": 64
          }
        ]
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```

* for client

```json
{
  "log": {
    "error": "",
    "loglevel": "info",
    "access": ""
  },
  "inbounds": [
    {
      "listen": "127.0.0.1",
      "protocol": "socks",
      "settings": {
        "udp": false,
        "auth": "noauth"
      },
      "port": "1080"
    },
    {
      "listen": "127.0.0.1",
      "protocol": "http",
      "settings": {
        "timeout": 360
      },
      "port": "1087"
    }
  ],
  "outbounds": [
    {
      "mux": {
        "enabled": false,
        "concurrency": 8
      },
      "protocol": "vmess",
      "streamSettings": {
        "tcpSettings": {
          "header": {
            "type": "none"
          }
        },
        "tlsSettings": {
          "allowInsecure": true
        },
        "security": "none",
        "network": "tcp"
      },
      "tag": "proxy",
      "settings": {
        "vnext": [
          {
            "address": "8.210.228.39",
            "users": [
              {
                "id": "39f91024-f331-46d8-90e5-4046a05bea77",
                "alterId": 64,
                "level": 0,
                "security": "auto"
              }
            ],
            "port": 1027
          }
        ]
      }
    }
  ],
  "dns": {},
  "routing": {
    "settings": {
      "domainStrategy": "AsIs",
      "rules": []
    }
  },
  "transport": {}
}
```

you just need to change the id ,port and IP address to your owns, but make sure that client are the same with server.

to get the uuid ,you can use this command on Cent OS.

```bash
cat /proc/sys/kernel/random/uuid
```

or you can visit the website to get one uuid.

[uuid generator](https://www.uuidgenerator.net/)

## fifth

done. 