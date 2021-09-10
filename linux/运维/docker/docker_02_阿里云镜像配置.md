阿里云[dockerCDN](dev.aliyun.com)

**加速器地址**

```
https://xxxxxxxx.mirror.aliyuncs.com
```

#### 配置镜像加速器

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://xxxxxx.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

