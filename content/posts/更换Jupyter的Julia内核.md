---
title: 更换Jupyter的Julia内核
date: 2021-02-8T11:59:30.000+08:00
tags: 
- Julia

---

> 在更新了Julia版本之后,使用IJulia会启动旧内核,如果删除了旧版本Julia,那么会出现无法启动内核的问题

__[请看这里](https://julialang.github.io/IJulia.jl/stable/manual/installation/)__

__还是那句话,先看文档__

### 第一步

这次我就直接显示我的名称啦~

```shell
hattoemi@hattoemi-Thurley:~$ jupyter kernelspec list
Available kernels:
  julia-1.5           /home/hattoemi/.local/share/jupyter/kernels/julia-1.5
  python3             /usr/local/share/jupyter/kernels/python3
hattoemi@hattoemi-Thurley:~$ jupyter kernelspec remove julia-1.5
```

### 第二步

打开Julia

```sh
               _
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.6.0-rc1 (2021-02-06)
 _/ |\__'_|_|_|\__'_|  |  Official https://julialang.org/ release
|__/                   |

julia> using IJulia

julia> installkernel("Julia")

```

__其重点在于`installkernel("Julia")`,它将会在Jupyter中安装一个叫"Julia-1.6"的内核,并自动索引到现在你机器上的Julia版本__

填在`installkernel("这里")`的内容只会决定内核的名字,空格会被"-"替代,这里并不影响安装的内核版本



***

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。