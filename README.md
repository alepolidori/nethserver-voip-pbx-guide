# NethServer VoIP PBX guide

This guide aims to help the administrator to install and configure a working [VoIP PBX](http://docs.nethserver.org/en/v7/freepbx.html?highlight=pbx) using [NethServer](http://www.nethserver.org/) distro Linux.

The configuration process is reduced to a minimal number of steps to produce only three extensions ready to use.

## Installation & configuration

### Step 1: download Nethserver ISO

Download NethServer ISO from [here](http://www.nethserver.org/getting-started-with-nethserver/).

### Step 2: install NethServer

You can install NethServer in "Unattended" mode:

1. launch the installation
1. choose "Other NethServer installation methods"
1. choose "Unattended installation"

entire installation process runs itself until the end.

### Step 3: show server IP

1. login as "root" with password "Nethesis,1234"
1. show IP with ```ifconfig``` command

### Step 4: configure NethServer using the wizard

1. go to the web interface https://<server_ip>:980
1. login as "root" and "Nethesis,1234" as credentials
1. complete the wizard (set your "Fully qualified domain name")

### Step 5: install VoIP PBX

1. go to the web interface https://<server_ip>:980
1. go to "Software center"
1. select "VoIP PBX" and the item "nethserver-janus"
1. click "ADD"
1. click "APPLY CHANGES"

### Step 6: download pbx configuration into the server

1. ssh into the server using "root" as username and the password chosen in the wizard
```
ssh root@<SERVER_IP>
```
2. download the pbx configuration
```
cd /root && wget https://raw.githubusercontent.com/alepolidori/nethserver-voip-pbx-guide/master/pbx_config.sql
```
3. execute
```
/usr/bin/mysql --force asterisk < pbx_config.sql 2> /dev/null && /usr/bin/scl enable rh-php56 "/usr/sbin/fwconsole reload"
```

## How to use

At the end of the "installatation & configuration" you have a working VoIP PBX with only three PJSIP extensions ready to use.
You can register any physical, softphone or webrtc phone and make your test.

It is possible to connect NethServer VoIP PBX to the external PSTN network to call any analogue or mobile phone, but a more advanced configuration is needed.

## Other info

NethServer VoIP PBX is the open source part of [NethVoice PBX](https://www.nethvoice.it/?lang=en) produced by [Nethesis.](http://www.nethesis.it/)

## Links

- NethServer FreePBX: http://docs.nethserver.org/en/v7/freepbx.html
- NethServer community: https://community.nethserver.org/
- NethServer repo:
   - https://github.com/NethServer/nethserver-freepbx
   - https://github.com/NethServer/freepbx
- Enterprise product: [NethVoice](https://www.nethvoice.it/?lang=en)
