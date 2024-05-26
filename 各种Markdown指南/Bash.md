# Shell 通用快捷键

- **Ctrl + K**: 删除光标到行末的所有内容。
- **Ctrl + U**: 删除光标到行首的所有内容。
- **Ctrl + W**: 删除光标前的一个单词。
- **Ctrl + Y**: 粘贴最近使用 Ctrl+K, Ctrl+U, 或 Ctrl+W 删除的文本。

 

# Linux系统文件介绍

## 1. /etc/passwd  文件 存储了 `：分隔的系统中所有用户的账户信息 根据GID可以判断是否为普通用户`

```bash
chenshuo:x:2048:1003::/data/user/chenshuo:/usr/bin/bash
```

$1:用户名

$2:加密密码

$3:用户ID

$4 ：分组ID   

- 系统用户和服务账户的组ID小于等于1000,如root用户组ID是0。
- 普通用户账户的组ID大于1000。这个范围内的组ID代表普通用户。

$5:用户信息 此字段一般为空，可以作为判断是哪个字段的标志

$6：用户主目录

$7: 用户登录时使用的shell， 此处 不同用户类型得到的权限不同

```bash
awk 'if($NF=='/bin/bash'){print}' /etc/passwd
```



在`Wheat2` 上进行统计查询

18 /bin/bash      1 /bin/sh      1 /bin/sync      1 /sbin/halt     62 /sbin/nologin      1 /sbin/shutdown     59 /usr/bin/bash 我统计了下系统中这些用户登录时使用的shell的类型，请问为什么不同用户登录时使用的shell不同呢？

使用/bin/bash 的shell的用户 

      1 amandabackup:x:33:6:Amanda user:/var/lib/amanda:/bin/bash
      1 chaill:x:1017:10::/data/user/chaill:/bin/bash
      1 chenym:x:1019:10::/data/user/chenym:/bin/bash
      1 liud:x:1020:10::/data/user/liud:/bin/bash
      1 liuj:x:1013:10::/data/user/liuj:/bin/bash
      1 liutp:x:1036:1003::/data2/user2/liutp/:/bin/bash
      1 postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
      1 qinz:x:1022:10::/data/user/qinz:/bin/bash
      1 root:x:0:0:root:/root:/bin/bash
      1 rstudio-server:x:379:377::/home/rstudio-server:/bin/bash
      1 shinyug:x:1024:1002::/data/user/shinyug:/bin/bash
      1 slurm:x:2015:2015::/home/slurm:/bin/bash
      1 songl:x:1021:10::/data/user/songl:/bin/bash
      1 wangyf:x:1008:10::/data/user/wangyf:/bin/bash
      1 wangzh:x:1001:1000::/home/wangzh:/bin/bash
      1 weilong:x:1004:1000::/home/weilong:/bin/bash
      1 yangzz:x:1025:10::/data/user/yangzz:/bin/bash
      1 zhangzh:x:1047:1003::/data2/user2/zhangzh:/bin/bash

## 2. /etc/fstab 定义了文件系统的挂载信息

挂载的文件系统分为物理文件系统XFS（如硬盘分区 `/dev/sda1`）和网络文件系统NFS（如 NFS 挂载 `192.168.100.103:/data3`）

dev/sd*开头的表示 物理设备

```tex
#
# /etc/fstab
# Created by anaconda on Fri Mar 24 10:37:06 2017
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=8ed85b9a-566c-4ccb-abfd-e163c12f1b6e /           xfs     defaults        0 0
UUID=3466c11d-5588-4d7d-a642-387133bcaadf /data       xfs     defaults,usrquota,grpquota        0 0
UUID=852bc7bb-1711-4a8e-9fae-096212dc134c /home       xfs     defaults,usrquota,grpquota        0 0
#UUID=9ea83e1d-b9e3-4e52-aee8-c70635e0de6d swap        swap    defaults        0 0
192.168.100.102:/data2   /data2   nfs     nfsvers=3,mountproto=tcp,rw,soft,rsize=1048576,wsize=1048576,noatime,nodiratime,nolock,async,timeo=600,_netdev      0       0
192.168.100.103:/data3   /data3   nfs     nfsvers=3,mountproto=tcp,rw,soft,rsize=1048576,wsize=1048576,noatime,nodiratime,nolock,async,timeo=600,_netdev      0       0
192.168.100.104:/data4   /data4   nfs   nfsvers=3,mountproto=tcp,rw,soft,noatime,nolock,nodiratime,async,rsize=1048576,wsize=1048576,timeo=600,_netdev       0       0
```

## 3. df -h   显示所有挂载的文件系统的磁盘使用情况 `Mounted on为挂载位置`



```te
Filesystem              Size  Used Avail Use% Mounted on
devtmpfs                189G     0  189G   0% /dev
tmpfs                   189G  660M  189G   1% /dev/shm
tmpfs                   189G  4.0G  185G   3% /run
tmpfs                   189G     0  189G   0% /sys/fs/cgroup
/dev/sda1               101G   49G   53G  48% /
/dev/sdb1                19T   16T  2.5T  87% /home
/dev/sdb3                22T   21T  1.3T  95% /data
tmpfs                    38G  4.0K   38G   1% /run/user/1022
tmpfs                    38G  4.0K   38G   1% /run/user/1025
tmpfs                    38G     0   38G   0% /run/user/1024
tmpfs                    38G     0   38G   0% /run/user/1006
tmpfs                    38G     0   38G   0% /run/user/2008
tmpfs                    38G     0   38G   0% /run/user/2011
tmpfs                    38G  4.0K   38G   1% /run/user/2024
tmpfs                    38G  4.0K   38G   1% /run/user/1047
tmpfs                    38G  4.0K   38G   1% /run/user/1038
192.168.100.103:/data3  137T  125T   13T  91% /data3
tmpfs                    38G     0   38G   0% /run/user/2014
tmpfs                    38G     0   38G   0% /run/user/2007
tmpfs                    38G     0   38G   0% /run/user/2034
192.168.100.104:/data4  146T  134T   13T  92% /data4
tmpfs                    38G     0   38G   0% /run/user/2029
tmpfs                    38G     0   38G   0% /run/user/2003
tmpfs                    38G     0   38G   0% /run/user/2016
tmpfs                    38G  4.0K   38G   1% /run/user/2032
tmpfs                    38G   44K   38G   1% /run/user/0
tmpfs                    38G     0   38G   0% /run/user/2048
tmpfs                    38G     0   38G   0% /run/user/1041
tmpfs                    38G  4.0K   38G   1% /run/user/1001
192.168.100.102:/data2   99T   93T  5.5T  95% /data2
tmpfs                    38G     0   38G   0% /run/user/2044
tmpfs                    38G     0   38G   0% /run/user/2036
tmpfs                    38G  4.0K   38G   1% /run/user/2050
tmpfs                    38G     0   38G   0% /run/user/2049
tmpfs                    38G     0   38G   0% /run/user/2002
tmpfs                    38G     0   38G   0% /run/user/1035
tmpfs                    38G     0   38G   0% /run/user/2035
tmpfs                    38G     0   38G   0% /run/user/2055
tmpfs                    38G     0   38G   0% /run/user/2027
tmpfs                    38G     0   38G   0% /run/user/2046
```



## 4. netstat -tan

用于显示网络连接、路由表、接口统计等网络状态信息。

- `-t`：表示显示TCP连接。

- `-a`：表示显示所有选项，默认不显示LISTEN相关和PCB绑定但未使用的连接。

- `-n`：表示显示数字形式的地址和端口号，不进行域名解析。

  TCP协议的这些状态

      1 CLOSE_WAIT 连接的一端已经关闭（通常是客户端），另一端（通常是服务器）尚未关闭连接。
    384 ESTABLISHED 连接已经建立，数据可以在这个连接上进行传输。
      1 FIN_WAIT1 连接的一端已经发送了FIN（结束）包，请求关闭连接，正在等待对方的确认。
      3 FIN_WAIT2 未在列表中，但在FIN_WAIT1之后，如果收到对方的确认，将进入此状态。
     91 LISTEN 服务器端的监听状态，等待客户端的连接请求
      1 SYN_SENT 客户端尝试连接服务器时发送了SYN（同步序列编号）包，正在等待服务器的响应。
     82 TIME_WAIT 连接已经关闭，但等待足够的时间以确保所有的数据包都被接收，防止连接重启时发生数据包混淆
     请注意，TCP连接的状态转换是复杂的，涉及到多个步骤，如三次握手（SYN、SYN-ACK、ACK）和四次挥手（FIN、ACK、FIN、ACK）。每个状态都反映了连接在建立、数据传输和关闭过程中的特定阶段。在实际的网络管理中，了解这些状态对于诊断网络问题和优化网络性能非常重要

# 文件操作

## 排除删除

删除除了moni.vcf文件以外的文件

```bash
rm `ls *moni* | grep -v moni.vcf`
# 启动排除模式删除
rm -f !(^file1$|^file2$)*
```

## 快速创建文件，使用Ctrl+D结束输入

```bash
 cat > tmp.txt
```



# 前台后台

jobs
[1]+  Stopped                 less -S hha.txt

进程被挂起了的话使用`fg %1` 恢复到前台

`bg %1` 作业恢复到后台  且终端不会显示其输出

`bg %1 &` 作业恢复到后台 终端能够查看其输出



# parallel并发

14min 189个Gene

```bash
# 每四个文件四个文件进行压缩
parallel -j 4 gzip ::: $(cat files.txt)
cat files.txt |  parallel -j 4 'gzip {}'
```





# 脚本常用变量

$Home 保存用户家目录

$PWD 保存当前工作目录



# Bash 程序控制

## 条件

```bash
if [ condition ]
then
    # Commands to execute if the condition is true
elif [ another_condition ]
then
    # Commands to execute if the first condition is false and the second condition is true
else
    # Commands to execute if both the above conditions are false
fi
```

## 循环



# awk

https://www.youtube.com/watch?v=Z95bj6AVa_8

1h06min

## 基础

 1. awk -F ':' -v var=mage -f [符合awk格式的脚本文件] 

 2. awk -F ':' -v var=mage -f ‘BEGIN{ACTION}pattern{action}END{ACTION}’ file...

    FS

    OFS

    RS

    ORS

    

    NF     

    $NF 	

    $1

    

    NR

    FNR

    FILENAME

    ```bash
    # BEGIN{} 例子
    awk 'BEGIN{test=70;if(test>90){print "very good"} else if(test>60){print "good"} else{print"no pass"} } '
    ```

    

## awk正则表达

^行首

*任意个任意字符

[[:space:]]任意单个空白字符（包括空格、制表符、换行符等）

[[:space:]]+ 任意多个空白字符

^[0-9]数字开头的



```bash
awk '/^[[:space:]]*linux16/{i=1;while(i<=NF) {print $i,length($i);i++} }' /etc/grub2.cfg
#实际上找出某一行，每个单词拿出来再统计每个单词的长度

awk '/^[[:space:]]*linux16/{i=1;while(i<=NF) { if(length($i)>=10) {print $i,length($i)};i++} }' /etc/grub2.cfg
```

> 本地的`/etc/grub2.cfg`文件我无权访问，故随机生成了一个该文件

```bash
# GRUB2 sample configuration file
#
# Attention: manual changes to this file may cause system boot issues.
# This file is generated automatically, any changes will be overwritten.

set default="0"
set timeout=5
set hiddentimeout=0

menuentry "Ubuntu 20.04 LTS" {
    multiboot /boot/vmlinuz-5.4.0-42-generic
    module /boot/initrd.img-5.4.0-42-generic initrd
    module /boot/System.map-5.4.0-42-generic System.map
    bootparams "root=UUID=1234-5678 ro quiet splash"
}

menuentry "Advanced options for Ubuntu" {
    menuentry "Ubuntu, with Linux 5.4.0-42-generic (recovery mode)" --class ubuntu {
        set gfxpayload=keep
        insmod gzio
        insmod part_gpt
        insmod ext2
        insmod linux
        linux /boot/vmlinuz-5.4.0-42-generic root=UUID=1234-5678 ro single
        initrd /boot/initrd.img-5.4.0-42-generic
    }
    # Other advanced options can be added here
}

menuentry "Memory Test (Memtest86+)" {
    insmod gzio
    insmod part_gpt
    insmod ext2
    set root=(hd0,gpt2)
    linux16 /boot/memtest86+.bin
}

# This file was generated by GRUB2's bootlace command.
# Do not edit this file. Changes will be overwritten.
```





## awk控制语句 (有点像java)： else后多条语句的时候需要用`{}`括起来表示执行这块中的所有语句 ；对于字段一个一个处理的时候使用while，行是用不到的(`行自带循环`)





```bash
# 组合语句
{statements;...}组合语句 

# if else 分支
if(condition){statements;...} 
if(condition1){statements1} else if(condition2){statements2} else {statements3}
awk -F: '{if($3>1000) {printf "Common user:%s\n",$1} else{printf "root or Sysuser:%s\n",$1} }' /etc/passwd

# while 循环  对于字段一个一个处理的时候使用while，行是用不到的(行自带循环) 例子在正则出现过
while(condition){statements;...}
awk '/^[[:space:]]*linux16/{i=1;while(i<=NF) { if(length($i)>=10) {print $i,length($i)};i++} }' /etc/grub2.cfg 


# do while 循环 
do{statements;...} while(condition)

# for循环
for(expr1;expr2;expr3) {statements;...}
awk -v sum=0 'BEGIN{ for(i=1;i<=100;i++) {sum+=i};print sum }'

# switch语句

# break

# continue

# next提前结束对本行的处理，直接进入下一行 （awk自身循环，类似于continue）

awk -F: '{if($3>10)print$1,$3;if($3<100)print $1,$3 }' /etc/passwd
  ----大于10或小于100的行打印一次
  
awk -F: '{if($3>10)print$1,$3} {if($3<100)print $1,$3 }' /etc/passwd
  ----大于10或者<100的行打印一次
  ----两者同时满足的行打印两次
  



delete array[index]

delete arry

exit
```

## awk数组

awk的数组就是关联数组 哈希

```bash


awk '!arr[$0]++'  
# 能够去掉重复的行
# 原理：空/0取反为1(true),任何数字取反均为false,空++是1


awk 'NR==FNR{fruit_name[$1]=$1;fruit_price[$1]=$2;next} {if($1==fruit_name[$1]){print $0,fruit_price[$1]} else{print $0,"noinfomation"}}' file1 file1.txt

```



## 行列转置

```bash
awk '{ for (i=1; i<=NF; i++) a[i,NR]=$i } NF>p { p=NF } END { for(j=1; j<=p; j++) { str=a[j,1]; for(i=2; i<=NR; i++) str=str" "a[j,i]; print str } }' GE.txt > tGE.TXT

awk '{for (i=1; i<=NF; i++) a[i,NR]=$i } NF>p {p=NF } END { 
			for(j=1; j<=p; j++) { 
				str=a[j,1];
				for(i=2; i<=NR; i++) {
					str=str" "a[j,i]
					};
				print str } 
			}' tmp.txt


```





## 遍历awk数组

```bash
awk 'BEGIN{grace["xiaoming"]="56";grace["lihua"]="99";grace["zhangfei"]="2";for (i in grace) {print grace[i]}}'
```

## 使用数组统计出现的次数

``` bash
#  netstat -tan| awk /^tcp/'{print $NF}' |sort|uniq -c
netstat -tan| awk /^tcp/'{state[$NF]++} END{for (i in state) {print i,state[i]}}' 

netstat -tan| awk /^tcp/'{state[$NF]++} END{for (i in state) if(state[i]==1){print i,state[i]}}' 
```

数组的用处

```bash
# 找出所有的访问次数大于1000的IP地址，决绝这些玩意的访问
for i in `awk '{IP[$1]++} END{for(i in IP)if(IP[i]>1000){print i} }' /var/log/httpd/access_log`; do
iptables -A INPUT -s $i -j REJECT
done

awk '{IP[$1]++} END{for(i in IP)if(IP[i]>1000){print i} }' /var/log/httpd/access_log | while read ip;do
iptables -A INPUT -s $ip -j REJECT
done

```



for i in

## printf

```bash
awk -F: '{if($3>1000) {printf "Common user:%s\n",$1} else{printf "root or Sysuser:%s\n",$1} }' /etc/passwd
```

- /etc/passwd文件中
- 系统用户和服务账户的组ID小于等于1000,如root用户组ID是0。
- 普通用户账户的组ID大于1000。这个范围内的组ID代表普通用户。

```tex

{printf "格式", $i}
"%s\t"
"%.2f\t"
"%.2f%%\t",$i*100
printf "10s\t"
	%10s %3s %10.2f %3.2f
	字段一共占几个字节，不足在左侧补充空格，
	另外，比如zhangbaoyue一共占11个字节，我设置%10s以下字节对字段是没有任何影响效果的，
	然后如果设置%20s,就会在左侧补充空格，
	产生右对齐效果
	
	%-10s %-3s %-10.2f %-3.2f
	右侧补充空格，
	产生左对齐效果
	注意：一定要设置超过原始字段的长度，否则无法产生对齐效果
printf ">%s\n", substr($1,2);printf "\n"}
	某一列的内容单独进行操作，比如这里对第一列，从第二个字符串开始
	

```



## length()函数 计算字符（不是字节空间）的数量，一个汉字也是一个字符，

## 外部变量引入awk

```bash
1. awk 'BEGIN{print length(ENVIRON["PWD"])}'
2. awk -v name="$PWD" 'BEGIN{print name}'
```

# shell的花括号扩展（brace expansion） `建议使用printf`

```bash
for chr in chr{1..7}{A,B,D};do printf "%s\n" $chr ;done
```

```tex
chr1A
chr1B
chr1D
chr2A
chr2B
chr2D
chr3A
chr3B
chr3D
chr4A
chr4B
chr4D
chr5A
chr5B
chr5D
chr6A
chr6B
chr6D
chr7A
chr7B
chr7D
```

```bash
printf "%s\n" chr{1..7}{A,B,D}
printf "%s " chr{1..7}{A,B,D}
# => echo -n chr{1..7}{A,B,D}
echo  chr{1..7}{A,B,D} 
##最后一行有换行符
```









  





