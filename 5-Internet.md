## 网络故障排除命令
- ping
- traceroute
- mtr
- nslookup
- telnet
- tcpdump
- netstat
- ss

主机问题：
ping : 当前主机和目标主机是否畅通，ping 不通代表 网络中断或对方有防火墙
traceroute/mtr : 检测当前主机到目标主机网络状况，辅助 ping 来使用，如果 ping 目标主机是畅通的，访问还是出现异常，可能是中间的网络质量出现问题。traceroute命令可以追踪服务器的每一跳服务的质量，mtr检查到目标主机之间是否有数据包被丢失了。
nslookup:  域名方式访问，域名对应的ip 可以通过 nslookup 来解决

端口问题：
telnet :  主机可以连接，但是服务仍然不可用，可以用telnet 检查端口的连接状态
tcpdump: 端口通了，仍然有问题，需要更细致的分析这个数据包，需要 tcpdump 命令
netstat/ss : 如果数据包还是没问题，可能是我们服务提供的监听范围不对，如果我们只对 127.0.0.1 提供服务，其他 ip 访问肯定是访问不到我们的服务。
