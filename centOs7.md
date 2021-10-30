{
  "inbounds": [
    {
      "port": 443, // 建议使用 443 端口
      "protocol": "vmess",    
      "settings": {
        "clients": [
          {
            "id": "",  
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network": "tcp",
        "security": "tls", // security 要设置为 tls 才会启用 TLS
        "tlsSettings": {
          "certificates": [
            {
              "certificateFile": "/etc/v2ray/v2ray.crt", // 证书文件
              "keyFile": "/etc/v2ray/v2ray.key" // 密钥文件
            }
          ]
        }
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


{
  "inbounds": [
    {
      "port": 1080,
      "protocol": "socks",
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      },
      "settings": {
        "auth": "noauth"
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess",
      "settings": {
        "vnext": [
          {
            "address": "v2fly.nightowl.name", // tls 需要域名，所以这里应该填自己的域名
            "port": 443,
            "users": [
              {
                "id": "",
                "alterId": 64
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "tcp",
        "security": "tls" // 客户端的 security 也要设置为 tls
      }
    }
  ]
}



curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-dat-release.sh

bash install-release.sh
bash install-dat-release.sh

# firewall-cmd --zone=public --permanent --add-service=http
# firewall-cmd --zone=public --permanent --add-service=https
# firewall-cmd --reload

#教程地址
https://toutyrater.github.io/advanced/tls.html

curl  https://get.acme.sh | sh

yum install socat

~/.acme.sh/acme.sh --register-account -m v138468@gmail.com

~/.acme.sh/acme.sh --issue -d v2fly.nightowl.name --standalone --keylength ec-256 --force
~/.acme.sh/acme.sh --issue -d www.nightowl.name --standalone --keylength ec-256 --force
~/.acme.sh/acme.sh --issue -d nightowl.name --standalone --keylength ec-256 --force

sudo ~/.acme.sh/acme.sh --installcert -d v2fly.nightowl.name --ecc --fullchain-file /etc/v2ray/v2ray.crt --key-file /etc/v2ray/v2ray.key
sudo ~/.acme.sh/acme.sh --installcert -d www.nightowl.name --ecc --fullchain-file /etc/nginx/conf.d/ca/www.crt --key-file /etc/nginx/conf.d/ca/www.key
sudo ~/.acme.sh/acme.sh --installcert -d nightowl.name --ecc --fullchain-file /etc/nginx/conf.d/ca/.crt --key-file /etc/nginx/conf.d/ca/.key

chown -R nobody /etc/v2ray/
chown -R nobody /var/log/v2ray/

vim /usr/local/etc/v2ray/config.json


#这个是安装bbr用的
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh


====================================
history -c
> /var/log/lastlog
>/var/log/btmp
>/var/log/wtmp
