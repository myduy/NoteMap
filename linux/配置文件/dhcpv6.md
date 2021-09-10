> DHCPv6服务器配置文件示例 
> 来自用于TAHI测试使用的文件

> IPv6地址有效使用期
> （最后这个地址是不再可用由客户端）
>  (通常IPv6默认设置为30天）
```shell
default-lease-time 2592000;
```
> IPv6地址优先使用期
>  (最后这个地址是不支持 i.e., 这个客户端应该用其他地址给新连接)
>  (通常IPv6默认设置到7天)
```shell
preferred-lifetime 604800;
```
> T1,续借前延迟
>  (默认1/2优先使用期)
>  (设置为1小时)
```shell
option dhcp-renewal-time 3600; 
```
> T2, 重新绑定请延迟 (如果续借失败)
>  (默认有 3/4 优先使用期)
>  (设置为2小时)
```shell
option dhcp-rebinding-time 7200;
```
> 开启 RFC 5007 支持 (和DHCPv4一样)
```shell
allow leasequery;
```
> 定义全局 域名服务器地址和域名搜索列表
```shell
option dhcp6.name-servers 3ffe:501:ffff:100:200:ff:fe00:3f3e;
option dhcp6.domain-search "test.example.com","example.com";
```

> 设置优先级 255 (最大), 为了避免等待 
> 当只有一个服务器，添加一个服务器
```shell
#option dhcp6.preference 255;
```
> 服务端命令开启快速提交(2个数据包交换)
```shell
#option dhcp6.rapid-commit;
```
> 信息请求刷新之前的延迟
>  (默认不刷新。最小值十分钟，最大值为一天)
>  (设置为六小时)
```shell
option dhcp6.info-refresh-time 21600;
```
> 租约文件路径
```shell
dhcpv6-lease-file-name "/var/lib/dhcpd/dhcpd6.leases";
```

> 静态定义(必须为全局)
```shell
host myclient {
	# 这个条目同于查找
	host-identifier option
		dhcp6.client-id 00:01:00:01:00:04:93:e0:00:00:00:00:a2:a2;

	# 固定地址
	fixed-address6 3ffe:501:ffff:100::1234;
	
	# 固定前缀
	fixed-prefix6 3ffe:501:ffff:101::/64;
	
	# 覆盖全局定义,
	# 只在资源(地址或前缀)分配时有效
	option dhcp6.name-servers 3ffe:501:ffff:100:200:ff:fe00:4f4e;
	
	# 调试 (查看条目语句何时生效)
	# (当收到一份匹配的请求记录“sol”)
	##if packet(0,1) = 1 { log(debug,"sol"); }
}

host otherclient {
        #如果客户端提供了一个包含这个MAC地址的DUID-LL或DUID-LLT，
        #那么这个主机条目很有可能被匹配。
        hardware ethernet 01:00:80:a2:55:67;
        fixed-address6 3ffe:501:ffff:100::4321;
}
```

> 子网所在的服务器会被附加
>  (i.e., 这个服务器拥有的地址会在这个子网)
```shell
subnet6 3ffe:501:ffff:100::/64 {
	# 两个地址可提供到客户端
	#  (三个客户端可能得不到有效地址)
	range6 3ffe:501:ffff:100::10 3ffe:501:ffff:100::11;

	# 使用整个 /64 前缀 for 临时地址
	#  (i.e., 直接应用 RFC 4941)
	range6 3ffe:501:ffff:100:: temporary;
	
	# 部分 /64 前缀可获得前缀授权 (RFC 3633)
	prefix6 3ffe:501:ffff:100:: 3ffe:501:ffff:111:: /64;
}
```
> 在中继代理后的第二个子网
```shell
subnet6 3ffe:501:ffff:101::/64 {
	range6 3ffe:501:ffff:101::10 3ffe:501:ffff:101::11;

	# 覆盖全局定义,
	# 只在资源(地址或前缀)分配时有效
	option dhcp6.name-servers 3ffe:501:ffff:101:200:ff:fe00:3f3e;

}
```
> 在中继代理链后的第三个子网
```shell
subnet6 3ffe:501:ffff:102::/64 {
	range6 3ffe:501:ffff:102::10 3ffe:501:ffff:102::11;
}
```