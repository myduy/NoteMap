1、安装PPTP

```shell
yum install pptpd  ppp
```

2、配置文件

#修改dns信息

```shell
vim /etc/ppp/options.pptpd
```


将它更改为你的dns服务地址（此处为百度和谷歌的dns）

```shell
ms-dns 180.76.76.76
ms-dns 8.8.8.8
```

3、vpn 账户密码

```
vim /etc/ppp/chap-secrets
```


设置 VPN账号 + 服务类型 + VPN密码 + IP

```shell
# Secrets for authentication using CHAP

# client        server  secret                  IP addresses

123 pptpd 012345 *
```

账户123密码012345

4、设置最大传输单元

```shell
vim /etc/ppp/ip-up

在命令符 [ -x /etc/ppp/ip-up.local ] && /etc/ppp/ip-up.local “$@” 后面添加 ifconfig ppp0 mtu 1472
```

5、配置pptp配置文件

```shell
vim /etc/pptpd.conf

localip 10.0.0.62

remoteip 172.16.1.100-110

localip ---本机公网ip地址

remoteip ---分配给客户端的地址,一般是内网网段地址
```

6、打开内核的ip 转发功能

```shell
vim /etc/sysctl.conf

编辑配置文件，添加 net.ipv4.ip_forward = 1 的配置，保存后退出。
运行 sysctl -p 使修改后的参数生效。
```

7、设置开机启动

```shell
#重启PPTP服务

systemctl restart pptpd

#配置开机自启

systemctl enable pptpd.service
```

8、打开防火墙

```shell
开启47及1723端口：

firewall-cmd --zone=public --add-port=47/tcp --permanent
firewall-cmd --zone=public --add-port=1723/tcp --permanent

允许防火墙伪装IP：

firewall-cmd --zone=public --add-masquerade

允许gre协议：

firewall-cmd --permanent --direct --add-rule ipv4 filter INPUT 0 -p gre -j ACCEPT
firewall-cmd --permanent --direct --add-rule ipv4 filter OUTPUT 0 -p gre -j ACCEPT

设置规则允许数据包由eth0和ppp+接口中进出

firewall-cmd --permanent --direct --add-rule ipv4 filter FORWARD 0 -i ppp+ -o eth0 -j ACCEPT
firewall-cmd --permanent --direct --add-rule ipv4 filter FORWARD 0 -i eth0 -o ppp+ -j ACCEPT

 设置转发规则，从源地址发出的所有包都进行伪装，改变地址，由eth0发出：（192.168.0.0内网地址，子网地址前两位）

firewall-cmd --permanent --direct --passthrough ipv4 -t nat -I POSTROUTING -o eth0 -j MASQUERADE -s 192.168.0.0/24

重启服务器：

firewall-cmd --reload
systemctl restart pptpd
```

9、日志

```shell
1、上线日志
vim /etc/ppp/ip-up

在[ -x /etc/ppp/ip-up.local ] && /etc/ppp/ip-up.local "$@" 后加上

echo "$PEERNAME 分配IP: $5 登录IP: $6 登录时间: `date -d today +%F_%T`" >> /var/log/pptpd.log

/2、下线日志
vim /etc/ppp/ip-down

在/etc/sysconfig/network-scripts/ifdown-post --realdevice ${REALDEVICE} \
    ifcfg-${LOGDEVICE}
后加上

echo "$PEERNAME 下线IP: $6 下线时间: `date -d today +%F_%T`" >> /var/log/pptpd.log
```

