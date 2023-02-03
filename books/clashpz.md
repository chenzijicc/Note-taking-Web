#### clash配置
#### plutotv分流配置



``` yaml
   
   
     -
       name: 'plutotv'
       type: select
       proxies: 
         - '🇺🇲 美国 01 [ B1 ] Trojan'
         - '🇺🇲 美国 02 [ B1 ] Trojan'
         - '🇺🇲 美国 03 [ B1 ] Trojan'
   rules:
   - DOMAIN-SUFFIX,pluto.tv,plutotv
   - DOMAIN-SUFFIX,hicloud.com,plutotv
   - DOMAIN-SUFFIX,googleapis.com,plutotv
```

#### Netflix分流配置
```
  # 🎬Netflix
  - DOMAIN-SUFFIX,netflix.com,🎬Netflix
  - DOMAIN-SUFFIX,netflix.net,🎬Netflix
  - DOMAIN-SUFFIX,nflxext.com,🎬Netflix
  - DOMAIN-SUFFIX,nflximg.com,🎬Netflix
  - DOMAIN-SUFFIX,nflximg.net,🎬Netflix
  - DOMAIN-SUFFIX,nflxso.net,🎬Netflix
  - DOMAIN-SUFFIX,nflxvideo.net,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest0.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest1.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest2.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest3.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest4.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest5.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest6.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest7.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest8.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest9.com,🎬Netflix
  - DOMAIN-SUFFIX,netflixdnstest10.com,🎬Netflix
  - DOMAIN-SUFFIX,netflix.com.edgesuite.net,🎬Netflix
  - DOMAIN-SUFFIX,us-west-2.amazonaws.com,🎬Netflix
  - DOMAIN-KEYWORD,dualstack.apiproxy-,🎬Netflix
  - DOMAIN-KEYWORD,apiproxy-device-prod-nlb-,🎬Netflix
  - DOMAIN-KEYWORD,ichnaea-web-,🎬Netflix
  - DOMAIN-KEYWORD,netflix,🎬Netflix
  - IP-CIDR,8.41.4.0/24,🎬Netflix,no-resolve
  - IP-CIDR,23.78.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,23.246.0.0/18,🎬Netflix,no-resolve
  - IP-CIDR,34.192.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,34.208.0.0/12,🎬Netflix,no-resolve
  - IP-CIDR,34.248.0.0/13,🎬Netflix,no-resolve
  - IP-CIDR,35.160.0.0/13,🎬Netflix,no-resolve
  - IP-CIDR,37.77.184.0/21,🎬Netflix,no-resolve
  - IP-CIDR,38.72.126.0/24,🎬Netflix,no-resolve
  - IP-CIDR,44.224.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,44.230.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,45.57.0.0/17,🎬Netflix,no-resolve
  - IP-CIDR,52.0.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,52.5.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,52.7.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,52.10.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,52.12.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,52.22.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,52.24.0.0/14,🎬Netflix,no-resolve
  - IP-CIDR,52.32.0.0/14,🎬Netflix,no-resolve
  - IP-CIDR,52.40.0.0/14,🎬Netflix,no-resolve
  - IP-CIDR,52.48.0.0/14,🎬Netflix,no-resolve
  - IP-CIDR,52.54.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,52.71.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,52.72.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,52.88.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,54.0.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,54.68.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,54.74.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,54.76.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,54.85.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,54.86.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,54.148.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,54.175.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,54.186.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,54.188.0.0/15,🎬Netflix,no-resolve
  - IP-CIDR,54.213.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,54.214.128.0/17,🎬Netflix,no-resolve
  - IP-CIDR,64.120.128.0/17,🎬Netflix,no-resolve
  - IP-CIDR,66.197.128.0/17,🎬Netflix,no-resolve
  - IP-CIDR,69.53.224.0/19,🎬Netflix,no-resolve
  - IP-CIDR,103.87.204.0/22,🎬Netflix,no-resolve
  - IP-CIDR,108.175.32.0/20,🎬Netflix,no-resolve
  - IP-CIDR,185.2.220.0/22,🎬Netflix,no-resolve
  - IP-CIDR,185.9.188.0/22,🎬Netflix,no-resolve
  - IP-CIDR,192.173.64.0/18,🎬Netflix,no-resolve
  - IP-CIDR,198.38.96.0/19,🎬Netflix,no-resolve
  - IP-CIDR,198.45.48.0/20,🎬Netflix,no-resolve
  - IP-CIDR,203.75.84.0/24,🎬Netflix,no-resolve
  - IP-CIDR,203.83.220.0/22,🎬Netflix,no-resolve
  - IP-CIDR,203.116.0.0/16,🎬Netflix,no-resolve
  - IP-CIDR,203.198.0.0/20,🎬Netflix,no-resolve
  - IP-CIDR,203.198.80.0/21,🎬Netflix,no-resolve
  - IP-CIDR,207.45.72.0/22,🎬Netflix,no-resolve
  - IP-CIDR,208.75.76.0/22,🎬Netflix,no-resolve
  - IP-CIDR,218.102.32.0/19,🎬Netflix,no-resolve
  - IP-CIDR,219.76.0.0/17,🎬Netflix,no-resolve
```

#### Disney+ 分流配置
```
  - DOMAIN-SUFFIX,disneyplus.com,🎞️Disney+
  - DOMAIN-SUFFIX,disney-plus.net,🎞️Disney+
  - DOMAIN-SUFFIX,disneystreaming.com,🎞️Disney+
  - DOMAIN-SUFFIX,dssott.com,🎞️Disney+
  - DOMAIN,playback-certs.bamgrid.com,🎞️Disney+
  - DOMAIN,disney.api.edge.bamgrid.com,🎞️Disney+
  - DOMAIN,disney.connections.edge.bamgrid.com,🎞️Disney+
  - DOMAIN,disney.content.edge.bamgrid.com,🎞️Disney+
  - DOMAIN,disney.playback.edge.bamgrid.com,🎞️Disney+
  - DOMAIN,cdn.registerdisney.go.com,🎞️Disney+
  - DOMAIN-SUFFIX,execute-api.us-east-1.amazonaws.com,🎞️Disney+
```

#### hulu分流配置
```
- DOMAIN-KEYWORD,hulu,hulu
- DOMAIN-SUFFIX,hulu.com,hulu
```

#### Telegram 分流配置
```
  - DOMAIN-SUFFIX,telegra.ph,🐸速蛙云
  - DOMAIN-SUFFIX,telegram.org,🐸速蛙云
  - IP-CIDR,91.108.4.0/22,🐸速蛙云
  - IP-CIDR,91.108.8.0/21,🐸速蛙云
  - IP-CIDR,91.108.16.0/22,🐸速蛙云
  - IP-CIDR,91.108.56.0/22,🐸速蛙云
  - IP-CIDR,149.154.160.0/20,🐸速蛙云
  - IP-CIDR6,2001:67c:4e8::/48,🐸速蛙云
  - IP-CIDR6,2001:b28:f23d::/48,🐸速蛙云
  - IP-CIDR6,2001:b28:f23f::/48,🐸速蛙云
```

#### 内网过滤
```
  - IP-CIDR,0.0.0.0/8,DIRECT
  - IP-CIDR,10.0.0.0/8,DIRECT
  - IP-CIDR,17.0.0.0/8,DIRECT
  - IP-CIDR,100.64.0.0/10,DIRECT
  - IP-CIDR,127.0.0.0/8,DIRECT
  - IP-CIDR,169.254.0.0/16,DIRECT
  - IP-CIDR,172.16.0.0/12,DIRECT
  - IP-CIDR,192.0.0.0/24,DIRECT
  - IP-CIDR,192.0.2.0/24,DIRECT
  - IP-CIDR,192.88.99.0/24,DIRECT
  - IP-CIDR,192.168.0.0/16,DIRECT
  - IP-CIDR,198.18.0.0/15,DIRECT
  - IP-CIDR,198.51.100.0/24,DIRECT
  - IP-CIDR,203.0.113.0/24,DIRECT
  - IP-CIDR,224.0.0.0/4,DIRECT
  - IP-CIDR,240.0.0.0/4,DIRECT
  - IP-CIDR,255.255.255.255/32,DIRECT
  - IP-CIDR6,::1/128,DIRECT
  - IP-CIDR6,fe80::/10,DIRECT
  - IP-CIDR6,fc00::/7,DIRECT
  - IP-CIDR6,ff00::/8,DIRECT
```


#### 最终规则
```
# 最终规则
      - GEOIP,CN,DIRECT
      - MATCH,Proxy
```
