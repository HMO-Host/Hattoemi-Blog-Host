---
title: Ubuntu优化指南
---
## 开关机速度

### 开机

> 启动速度逐渐变慢，不一定是因为启动的服务太多或服务启动太慢，也有可能是因为内核没有卸载
>
> **同时此操作也可以加快关机速度**

```sh
hattoemi@Hattoemi-Thurley:~$ uname -a
Linux Hattoemi-Thurley 5.8.0-45-lowlatency #51-Ubuntu SMP PREEMPT Fri Feb 19 15:11:12 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
```

**我已经删除了旧内核**

**你只需要注意自己的内核版本**

```sh
sudo apt-get remove linux-
```

点击`Tab`键

会弹出所有你已经安装的内核

```shell
sudo apt-get purge linux-headers-5.8.0-44*
sudo apt-get purge linux-modules-5.8.0-44*
```

**注意要卸载`headers`和`modules`**

最后

```sh
sudo apt-get autoremove
```

### 开机服务

```sh
systemd-analyze blame 
```

通过这个命令来查看开机时最耗时的服务

退出按`q`

一般受这两个服务影响

```shell
sudo systemctl mask plymouth-quit-wait.service 
# 如果你安装了docker，而且不怎么用它
sudo systemctl mask docker.service 
```

### grub载入时间

可以先到计算机的`/etc/default/`下

用你喜欢的编辑器打开`grub`

找到`GRUB_TIMEOUT=10`对划线`GRUB_TIMEOUT=4`

### 关机

查看`/var/log`下的`boot.log`文件

建议使用终端打开

> 以下命令适用于Ubuntu 20.10

```shell
cd ~/../../var/log/
sudo cat boot.log
```

发现不是绿的东西，比如

```shell
[DEPEND] Dependency failed for SSSD NSS Service responder socket.
[DEPEND] Dependency failed for SSSD…toFS Service responder socket.
[DEPEND] Dependency failed for SSSD PAC Service responder socket.
[DEPEND] Dependency failed for SSSD…vice responder private socket.
[DEPEND] Dependency failed for SSSD PAM Service responder socket.
[DEPEND] Dependency failed for SSSD SSH Service responder socket.
[DEPEND] Dependency failed for SSSD Sudo Service responder socket.
```

> 上面这些没有什么影响

和

```shell
[FAILED] Failed to listen on Docker Socket for the API.
See 'systemctl status docker.socket' for details.
```

> 因为我关闭了`docker`服务

**主要就是看情况处理，不会百度或者谷歌就永远解决不了问题**

## 性能调优

**不是笔记本就不要安装`tlp`!!!**

**不是笔记本就不要安装`tlp`!!!**

**不是笔记本就不要安装`tlp`!!!**

一旦安装了，你也无法挽回了，至少我没有找到解决方案

**建议安装`CPUFREQ`**

**网上各种抄袭文的源头**

[10条加速Ubuntu Linux的杀手级技巧| Linux中国](https://zhuanlan.zhihu.com/p/38632813)

## 建议做的事情

[安装完Ubuntu 20.04后要做的16件事| Linux中国](https://zhuanlan.zhihu.com/p/138157348)