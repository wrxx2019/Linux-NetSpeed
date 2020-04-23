# Linux-NetSpeed
```
见
https://github.com/ylx2016/Linux-NetSpeed/releases

手动下载安装BBR内核见
https://github.com/ylx2016/kernel/releases

方便国内使用 避免使用raw域名
不卸载内核版本 不会卸载除安装的内核以外的内核，安装多个内核可能会撑爆启动分区
可能需要自己手动调整内核启动项，建议VNC下操作
wget -N --no-check-certificate "https://github.000060000.xyz/tcpx.sh" && chmod +x tcpx.sh && ./tcpx.sh
或
wget -N "https://github.000060000.xyz/tcpx.sh" && chmod +x tcpx.sh && ./tcpx.sh
卸载内核版本，同原作者版本，删除安装内核以外的所有内核
wget -N --no-check-certificate "https://github.000060000.xyz/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
或
wget -N "https://github.000060000.xyz/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

反馈，提建议，捐赠
https://blog.ylx.me/archives/783.html

ubuntu16要换锐速支持的内核才装的上
sudo apt-get install linux-image-extra-4.4.0-47-generic
dpkg -l |grep linux-image
有的系统本身有多个内核存在，需要删多次
卸载列出的其他内核：
sudo apt-get purge linux-image-4.4.0-21-generic linux-image-extra-4.4.0-21-generic

查看当前系统所有内核：dpkg -l|grep linux-image | awk '{print $2}'
卸载其余内核：apt-get purge 其余内核名称
更新 grub 系统引导文件：update-grub
重启VPS：reboot

支持版本
for bbr
centos6,7,8
debian8.9.10
ubuntu16,18,19
锐速内核稍微更新
xanmod/Zen/BBR2 只添加了centos7,8 debian9,10

bbrplus降级到4.14.129
维持原来的支持版本 不再支持c6,c8;debian和ubuntu各版本安装问题和我无关

提示Abort kernel removal? 选择No

5.5内核及BBR2内核支持cake队列

双持bbr+锐速
bbr 添加
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p

编辑锐速文件
nano /appex/etc/config

检测代码有BUG，如果锐速正常 运行查看
bash /appex/bin/lotServer.sh status | grep "LotServer"

检查bbr 内核默认bbr算法不会有输出
lsmod | grep bbr

检查centos安装内核
grubby --info=ALL|awk -F= '$1=="kernel" {print i++ " : " $2}'

查看当前支持TCP算法
cat /proc/sys/net/ipv4/tcp_allowed_congestion_control
查看当前运行的算法
cat /proc/sys/net/ipv4/tcp_congestion_control
查看当前队列算法
sysctl net.core.default_qdisc

命令： uname -a
作用： 查看系统内核版本号及系统名称

命令： cat /proc/version
作用： 查看目录"/proc"下version的信息，也可以得到当前系统的内核版本号及系统名称

真实队列查看？ 更改队列算法可能需要重启生效
tc -s qdisc show

bbsplus算法原作者
https://blog.csdn.net/dog250/article/details/80629551
bbrplus首用名 ？
https://github.com/cx9208/bbrplus
xanmod官网
https://xanmod.org
Zen官网
https://liquorix.net/
锐速
https://moeclub.org/2017/03/09/14/
