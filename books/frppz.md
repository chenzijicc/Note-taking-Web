#### frp配置
```text
# 服务器配置
[common]
# frp监听的端口，默认是7000，可以改成其他的
bind_port = 7000
# 授权码，请改成更复杂的
token = 52010  # 这个token之后在客户端会用到

# frp管理后台端口，请按自己需求更改
dashboard_port = 7500
# frp管理后台用户名和密码，请改成自己的
dashboard_user = admin
dashboard_pwd = admin
enable_prometheus = true

# frp日志配置
log_file = /var/log/frps.log
log_level = info
log_max_days = 3


# 客户端配置
[common]
server_addr = 服务器ip
 # 与frps.ini的bind_port一致
server_port = 7000
 # 与frps.ini的token一致
token = 52010

# 配置ssh服务
[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
 # 这个自定义，之后再ssh连接的时候要用
remote_port = 6000 

# 配置http服务，可用于小程序开发、远程调试等，如果没有可以不写下面的
[web]
type = http
local_ip = 127.0.0.1
local_port = 8080
# web域名
subdomain = test.hijk.pw
# 自定义的远程服务器端口，例如8080
remote_port = 8080
```