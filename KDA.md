# Kadena

# 节点安装参考
- https://github.com/kadena-io/chainweb-node#installing-chainweb

# 硬件要求
- 2 CPU cores
- 4 GB of RAM
- 250 GB SSD or fast HDD
- Public IP address

## 安装节点命令
- sudo apt-get install ca-certificates libgmp10 libssl1.1 libsnappy1v5 libtbb2 zlib1g liblz4-1 libbz2-1.0 libgflags2.2 zstd
- mkdir /data/.kadena && cd /data/.kadena
- wget https://github.com/kadena-io/chainweb-node/releases/download/2.17.1/chainweb-2.17.1.ghc-8.10.7.ubuntu-20.04.aaf1a20.tar.gz
- tar -zxvf chainweb-2.17.1.ghc-8.10.7.ubuntu-20.04.aaf1a20.tar.gz

### 生成配置文件并修改(如需要)
- ./chainweb-node --print-config > config.yaml
- databaseDirectory: /data/.kadena/block

### 注意
```
p2p端口1789对公网开放，API端口1848对相关服务器开放
```

# supervisor配置
```
[program:kadena]
command         = /data/.kadena/chainweb-node --config-file=/data/.kadena/config.yaml
directory       = /data/.kadena
autostart       = true
autorestart     = true
stdout_logfile  = /var/log/kadena.log
stderr_logfile  = /var/log/kadena.log
redirect_stderr = true
stopsignal      = QUIT
```

# start
- supervisorctl update
- supervisorctl start kadena

# 其他命令
- supervisorctl restart kadena
- supervisorctl stop kadena
- curl -sk "https://<public-ip>:<port>/chainweb/0.0/mainnet01/cut"
