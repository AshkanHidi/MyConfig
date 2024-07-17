{
  "dns": {
    "hosts": {
      "geosite:category-porn": "127.0.0.1",
      "domain:googleapis.cn": "googleapis.com"
    },
    "servers": [
      "1.1.1.1"
    ]
  },
  "inbounds": [
    {
      "listen": "127.0.0.1",
      "port": 10808,
      "protocol": "socks",
      "settings": {
        "auth": "noauth",
        "udp": true,
        "userLevel": 8
      },
      "sniffing": {
        "destOverride": [
          "http",
          "tls"
        ],
        "enabled": true
      },
      "tag": "socks"
    },
    {
      "listen": "127.0.0.1",
      "port": 10809,
      "protocol": "http",
      "settings": {
        "userLevel": 8
      },
      "tag": "http"
    }
  ],
  "log": {
    "loglevel": "warning"
  },
  "outbounds": [
    {
      "mux": {
        "concurrency": -1,
        "enabled": false,
        "xudpConcurrency": 8,
        "xudpProxyUDP443": ""
      },
      "protocol": "wireguard",
      "settings": {
        "address": [
          "172.16.0.2/32"
        ],
        "mtu": 1280,
        "peers": [
          {
            "endpoint": "2606:4700:d1::55e7:d6f3:b962:9705:987",
            "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo="
          }
        ],
        "reserved": [
          74,
          241,
          73
        ],
        "secretKey": "GLo8BVmxMvhkEkoPVHbBxsdCDuaLIe46ekBTChPd9GY="
      },
      "tag": "chain"
    },
{
      "protocol": "wireguard",
      "settings": {
        "secretKey": "oKGXW8p/HnQ5MwPU0wHLN804fvvYI4o5GtSou4Mr30k=",
        "address": [
          "172.16.0.2/32",
          "2606:4700:110:81ad:51b4:1efe:bd02:5e3b/128"
        ],
        "peers": [
          {
            "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
            "allowedIPs": [
              "0.0.0.0/0",
              "::/0"
            ],
            "keepAlive": 1,
            "endpoint": "162.159.195.13:8886"
          }
        ],
        "reserved": [
          14,87,148
        ],
        "mtu": 576
      },
      "proxySettings": {
        "tag": "chain"
      },
      "tag": "proxy"
    },
    {
      "protocol": "freedom",
      "settings": {},
      "tag": "direct"
    },
    {
      "protocol": "blackhole",
      "settings": {
        "response": {
          "type": "http"
        }
      },
      "tag": "block"
    }
  ],
  "remarks": "wireguard",
  "routing": {
    "domainStrategy": "IPIfNonMatch",
    "rules": [

      {
        "inboundTag": [
          "socks",
          "http",
         "dns-in"
        ],
        "outboundTag": "proxy",
        "type": "field"
      },
      {
        "ip": [
          "1.1.1.1"
        ],
        "outboundTag": "proxy",
        "port": "53",
        "type": "field"
      },
      {
        "domain": [
          "domain:ir",
          "geosite:category-ir",
          "geosite:private"
        ],
        "outboundTag": "direct",
        "type": "field"
      },
      {
        "ip": [
          "geoip:ir",
          "geoip:private"
        ],
        "outboundTag": "direct",
        "type": "field"
      },
      {
        "domain": [
          "geosite:category-porn"
        ],
        "outboundTag": "block",
        "type": "field"
      },
      {
        "ip": [
          "10.10.34.34",
          "10.10.34.35",
          "10.10.34.36"
        ],
        "outboundTag": "block",
        "type": "field"
      }
    ]
  }
}
