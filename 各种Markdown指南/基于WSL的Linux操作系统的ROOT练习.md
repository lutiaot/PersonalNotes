



> time命令简单介绍

这个命令 `time md5sum * > /data/user/chenshuo/data2/wheat_SNP/md5.txt` 执行了以下操作：

1. 使用 `md5sum` 命令计算当前目录下所有文件的 MD5 校验和。
2. 将计算结果重定向到 `/data/user/chenshuo/data2/wheat_SNP/md5.txt` 文件中。

命令前的 `time` 关键字是用于测量命令执行所需时间的工具。输出的时间包含了三个部分：

1. **real**: 这是实际经过的时间，也就是从命令开始执行到完全结束所花费的墙钟时间（wall-clock time）。它反映了完成整个过程真实感受到的时间，包括所有等待时间。在这个例子中，`real` 为 79 分钟和 32.077 秒。
2. **user**: 这是用户CPU时间，表示命令执行过程中花费在用户模式下的 CPU 时间总和。用户模式时间是指程序执行时消耗的 CPU 时间，不包括操作系统内核模式下的时间。在这个例子中，`user` 为 35 分钟和 23.739 秒。
3. **sys**: 这是系统CPU时间，表示命令执行过程中花费在系统模式（内核模式）下的 CPU 时间总和。系统模式时间是指操作系统为该程序提供服务时消耗的 CPU 时间，例如输入/输出操作。在这个例子中，`sys` 为 7 分钟和 39.453 秒。

综合来看，`real` 时间比 `user` 和 `sys` 时间总和要长得多，这表明在执行 `md5sum` 命令的过程中，可能存在大量的 I/O 等待时间（比如硬盘I/O），或者是因为系统负载较高导致的等待时间。`user` 时间和 `sys` 时间加起来大约为 43 分钟，这表示 CPU 实际上在这个任务上工作了 43 分钟，但整个过程却花费了近 79 分钟，这额外的时间就是等待时间。





# Bug汇总

>  在 WSL（Windows Subsystem for Linux）中使用 `yum` 命令安装htop提示 "No match for argument: htop" 错误

原因：

​	使用的是基于Oracle Linux的发行版（`oracle-linux-ol`），并且您想安装 `htop`，Oracle Linux 默认的仓库可能不包含 `htop` 这个软件包

解决：

1. 启用EPEL仓库：

EPEL（Extra Packages for Enterprise Linux）仓库为Oracle Linux提供额外的软件包。您可以通过以下命令安装EPEL仓库：

```bash
sudo yum install epel-release
```

2. ​	安装htop

```bash
sudo yum install htop
```



> 在Oracle Linux的终端中找不到 `clear` 命令

1. **未安装ncurses库**：`clear` 命令依赖于ncurses库。如果该库未安装，`clear` 可能不可用。您可以尝试安装ncurses库：

   ```bash
   sudo yum install ncurses
   ```

> Oracle可能不支持WSL 如果真的条件不足选择Centos 
>
> [基于Windwos11的WSL安装CentOS_wsl centos-CSDN博客](https://blog.csdn.net/qq_38442140/article/details/120724215)





