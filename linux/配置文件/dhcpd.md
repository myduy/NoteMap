# dhcpd.conf 配置文件解析

> 配置文件样本来自ISC dhcpd
>

> 对所有网络设置定义
>

```shell
option domain-name "example.org"; #设置域名
option domain-name-servers ns1.example.org, ns2.example.org; #设置域名服务器（设置DNS）


default-lease-time 600;#默认租期时间
max-lease-time 7200;#最大租期时间
```

> 开启/关闭 全局动态DNS 更新
>

```shell
ddns-update-style none; #动态更新方式 没有
```

> 如果这个DHCP服务器为本地网路正式（办公）DHCP服务器
>
> 则这个 “authoritave”  不应该被注释
>

```shell
authoritative; #授权
```

> 使用此命令发送日志消息到不同的日志文件中(你也可以对 syslog.conf 完成非法重定向)
>

```shell
log-facility local7;
```

>  没有服务这个子网将会被指定，但是要声明他来帮助DHCP服务器来了解网络拓扑
```shell
subnet 10.152.187.0 netmask 255.255.255.0 {
}
```
>  这是一个非常基础（简单）的子网声明
>

```shell
subnet 10.254.239.0 netmask 255.255.255.224 {
  range 10.254.239.10 10.254.239.20; #范围
  option routers rtr-239-0-1.example.org, rtr-239-0-2.example.org; #设置路由
}
```

>  这个声明运行BUUTP(引导协议)客户端获取地址
>  我们不是真正的推荐（我们并不建议这样）

```shell
subnet 10.254.239.32 netmask 255.255.255.224 {
  range dynamic-bootp 10.254.239.40 10.254.239.60; #动态bootp范围
  option broadcast-address 10.254.239.31; #设置广播地址
  option routers rtr-239-32-1.example.org; #设置路由
}
```

>  为一个内部子网进行细微的配置
>

~~~shell
subnet 10.5.5.0 netmask 255.255.255.224 {
  range 10.5.5.26 10.5.5.30; 
  option domain-name-servers ns1.internal.example.org; #设置DNS
  option domain-name "internal.example.org"; #设置域名
  option routers 10.5.5.1;  #设置路由地址
  option broadcast-address 10.5.5.31;#设置广播地址
  default-lease-time 600;#默认租期时间
  max-lease-time 7200;#最大租期时间
}
~~~

>  需要特殊配置选项的主机可以列在
>  主机语句里。如果没有指定地址，则地址会
>  动态分配(如果可以的话)，但是主机特定的信息
>  仍然来自主机的声明。
>

```shell
host passacaglia {
  hardware ethernet 0:0:c0:5d:bd:95; #硬件以太网
  filename "vmunix.passacaglia";  #文件名
  server-name "toccata.fugue.com"; #服务器名
}
```

>  固定ip地址也能对主机指定 ，
>  这些地址也不应该被列为有效的动态分配，
>  已指定固定IP地址的主机可以在BOOTP或DHCP使用，
>  只能未指定固定地址的主机使用DHCP启动，
>  除非子网上有一个地址范围有动态BOOTP标志的BOOTP客户端
> 连接到哪个集合。

```shell
host fantasia {
  hardware ethernet 08:00:07:26:c0:a5;
  fixed-address fantasia.fugue.com; #固定地址
}
```

>  您可以声明一个客户端类，然后以这个为依据进行地址分配。
>  下面的示例显示了所有客户机的情况在某个类上获得10.17.224/24子网上的所有地址其他客户端获得10.0.29/24子网上的地址。

```shell
class "foo" {
  match if substring (option vendor-class-identifier, 0, 4) = "SUNW";
}

shared-network 224-29 { 		#共享网络
  subnet 10.17.224.0 netmask 255.255.255.0 {
    option routers rtr-224.example.org;
  }
  subnet 10.0.29.0 netmask 255.255.255.0 {
    option routers rtr-29.example.org;
  }
  pool {
    allow members of "foo";
    range 10.17.224.10 10.17.224.250;
  }
  pool {
    deny members of "foo";
    range 10.0.29.10 10.0.29.230;
  }
}
```
