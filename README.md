# tcp_tsunami
tcp_tsunami adjust for kernel 4.13+（魔改版bbr，解决内核4.13+编译问题）
## How to use
1. Update your kernel to 4.13+. 更新您的内核至4.13+。
2. Install `make gcc`. 安装`make gcc`。
3. Run 执行:
```
wget https://raw.githubusercontent.com/liberal-boy/tcp_tsunami/master/tcp_tsunami.c
echo "obj-m:=tcp_tsunami.o" > Makefile
make -C /lib/modules/$(uname -r)/build M=`pwd` modules CC=/usr/bin/gcc
insmod tcp_tsunami.ko
cp -rf ./tcp_tsunami.ko /lib/modules/$(uname -r)/kernel/net/ipv4
depmod -a
modprobe tcp_tsunami
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=tsunami" >> /etc/sysctl.conf
sysctl -p
```
4. Check 检查 `sysctl net.ipv4.tcp_congestion_control`
