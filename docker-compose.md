##### - Compose Setup

<pre>
version: '3.8'

services:
    wireguard:
        container_name: wg-easy
        image: weejewel/wg-easy
        volumes:
            - /wireguard:/etc/wireguard
        env_file:
            - /wireguard/wireguard.env
        ports:
            - '61200:51820/udp'
            - '80:51821/tcp'
        cap_add:
            - NET_ADMIN
            - SYS_MODULE
        sysctls:
            - net.ipv4.ip_forward=1
            - net.ipv4.conf.all.src_valid_mark=1
        restart: unless-stopped
</pre>

##### - Env file
<pre>
WG_HOST=vpn.myserver.com`
WG_PORT=61820
WG_DEFAULT_DNS=1.1.1.1, 1.0.0.1
WG_ALLOWED_IPS=0.0.0.0/0, ::/0
PASSWORD=foobar123
</pre>
