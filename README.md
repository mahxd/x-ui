# x-ui ( V2ray + GUI-Panel )

Support multi-protocol multi-user XRAY panel

Translated version of https://github.com/vaxilu/x-ui

Thanks to https://github.com/NidukaAkalanka for tranlating web panel (other parts didn't work fine for me)

For Freedom

# Features

- System status monitoring
- Support multi-user multi-protocol, web page visualization operation
- Support protocol：vmess, vless, trojan, shadowsocks, dokodemo-door, socks, http
- Support configuration more transmission configuration
- Traffic statistics, restricting traffic, limit expiration time
- Can customize XRAY configuration template
- Support HTTPS access panel (self-reserve domain name + SSL certificate)
- Support the one-click SSL certificate application and automatically renew the visa
- More advanced configuration items, details

# Installation & upgrade

```
bash <(curl -Ls https://raw.githubusercontent.com/mahxd/x-ui-en/main/install.sh)
```

### Install server and config VMESS + WS

https://user-images.githubusercontent.com/85416927/202787833-7b093872-7ee0-48e6-85ee-ce6b208d9c70.mp4


### Add SSL to secure connection ( VMESS + WS + TLS )

https://user-images.githubusercontent.com/85416927/202795886-3f40140c-508b-4ef6-9a3c-f225ca0608f3.mp4


## Manual installation & upgrade

1. First go ot https://github.com/mahxd/x-ui-en/releases Download the latest compressed package, generally select the `AMD64` architecture
2. Then upload this compressed package to the server `/root/`In the directory and use `root`User login server

> If your server cpu The architecture is not `amd64`，The command will be in your own `amd64`Replace it with other architecture

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## Use docker installation

> This docker tutorial and Docker mirror image[Chasing66](https://github.com/Chasing66)supply

1. Install docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. Install x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```

> Build Your own image

```shell
docker build -t x-ui .
```

## SSLCertificate application

## SSLCertificate application
you can use LetsEncypt certificate generator with http at last step of setup(recommended).

or using following method (limited)

> This function and tutorial[FranzKafkaYu](https://github.com/FranzKafkaYu)supply

The script built -in SSL certificate application function, using this script application certificate, must meet the following conditions:

- Knowing Cloudflare registered mailboxes
- Know the Cloudflare Global API Key
- The domain name has been parsed to the current server through Cloudflare

Get cloudflare Global API Key method:
    ![](media/bda84fbc2ede834deaba1c173a932223.png)
    ![](media/d13ffd6a73f938d1037d0708e31433bf.png)

When you use it, you only need to enter the `domain name`, ` API Key`, the schematic diagram is as follows:
        ![](media/2022-04-04_141259.png)

Precautions:

- This script uses DNS API to apply for a certificate
- Use Let'sencrypt as a CA side by default
- Certificate installation directory is/root/cert directory
- This script application certificate is a pan-domain name certificate

## tg robot use (in development, not available for the time being)

> This function and tutorial are provided by [FranzkafKayu] (https://github.com/franzkafkkay)

x-ui supports daily traffic notifications, panel login reminders and other functions through tg robots. Using tg robots, you need to apply by yourself
For specific application tutorials, please refer to [Blog Link] (https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html)
Instructions for use: Set robot -related parameters in the background

- tg robot token
- tg robot Chatid
- tg robot cycle running time, use Crontab syntax

cron jobs：
- 30 * * * * * //Notification of each point 30s
- @hourly      //Notice per hour
- @daily       //Notice every day (at 0:00 in the morning)
- @every 8h    //Notice every 8 hours

tg notification content:
- Node traffic use
- Panel login reminder
- Node expires reminder
- Flow early warning reminder  

More functional planning...
## Suggestion system

- CentOS 7+
- Ubuntu 16+
- Debian 8+

# common problem

## from v2-ui migrate

First install the latest version of the x-ui on the v2-ui server, and then use the following command to migrate to migrate all the inbound account data of the migration of the v2-ui x-ui，`Panel settings and username passwords will not migrate`

> After the migration is successful, please turn off the v2-ui` and restart the x-ui`, otherwise the inbound of v2-ui will have the `port conflict with the inbound of x-ui.

```
x-ui v2-ui
```

## Issue closed

Various small white problems can see high blood pressure

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/vaxilu/x-ui)
