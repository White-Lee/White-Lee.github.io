---
title: TCP抓包
---

**安装**

```bash
# under centos
yum install tcpdump
# under Ubuntu
apt-get install tcpdump
```

**监视指定网络接口的数据包(一定要查看网卡)**

```bash
tcpdump -i eth1
```

**监视指定主机的数据包**

```bash
# 打印所有进入或离开sundown的数据包.
tcpdump host sundown
# 指定ip,例如截获所有210.27.48.1 的主机收到的和发出的所有的数据包
tcpdump host 210.27.48.1
# 打印helios 与 hot 或者与 ace 之间通信的数据包
tcpdump host helios and \( hot or ace \)
# 截获主机210.27.48.1 和主机210.27.48.2 或210.27.48.3的通信
tcpdump host 210.27.48.1 and \ (210.27.48.2 or 210.27.48.3 \) 
# 打印ace与任何其他主机之间通信的IP 数据包, 但不包括与helios之间的数据包.
tcpdump ip host ace and not helios
# 如果想要获取主机210.27.48.1除了和主机210.27.48.2之外所有主机通信的ip包，使用命令：
tcpdump ip host 210.27.48.1 and ! 210.27.48.2
# 截获主机hostname发送的所有数据
tcpdump -i eth0 src host hostname
# 监视所有送到主机hostname的数据包
tcpdump -i eth0 dst host hostname
```

**监视指定主机和端口的数据包**

```bash
# 如果想要获取主机210.27.48.1接收或发出的telnet包，使用如下命令
tcpdump tcp port 23 and host 210.27.48.1
# 对本机的udp 123 端口进行监视 123 为ntp的服务端口
tcpdump udp port 123 
```

**监视指定协议的数据包**

```bash
# 打印TCP会话中的的开始和结束数据包, 并且数据包的源或目的不是本地网络上的主机.(nt: localnet, 实际使用时要真正替换成本地网络的名字))
tcpdump 'tcp[tcpflags] & (tcp-syn|tcp-fin) != 0 and not src and dst net localnet'
# 打印所有源或目的端口是80, 网络层协议为IPv4, 并且含有数据,而不是SYN,FIN以及ACK-only等不含数据的数据包.(ipv6的版本的表达式可做练习)
tcpdump 'tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)'
```

