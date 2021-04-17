---
title: Julia1.6的更新过程
date: 2021-03-27T11:59:30.000+08:00
tags: 
- Julia

---

## 可喜可贺!可喜可贺啊!

__期待已久的Julia1.6版本终于在2021年3月25日(星期四)11：30正式发布了v1.6__

那么使用jill安装Julia的各位该怎么更新Julia呢?

其实没必要完全删除`.julia`文件夹

### 第一步

__如果是`1.6.0-rc*`则不需要这一步，`jill`会自动处理__

> Linux下只需要删除julias文件夹下的旧版本Julia即可

```sh
which julia
/usr/local/bin/julia
ll /usr/local/bin/julia
lrwxrwxrwx 1 root root 31  2月  7 12:29 /usr/local/bin/julia -> /opt/julias/julia-1.5/bin/julia*
sudo rm -rf /opt/julias/julia-1.5
```

### 第二步

> 通过jill安装Julia v1.6

```shell
sudo jill install 1.6.0
```

静候安装~

### 第三步

__如果是`1.6.0-rc*`则不需要这一步__

> __以前安装的包肯定还在的,但是为什么再新版本的Julia里面using不了?__
>
> __这个时候肯定有同学选择直接删除`.julia`文件夹__
>
> __但其实只不过是因为Julia自己的`Manifest.toml`和`Project.toml`用`v1.5`和`v1.6`分开了而已__

命令行下

```shell
cd .julia/environments/v1.5
cp * ../v1.6
cd ../
rm -rf v1.5/
cd ../compiled/
rm -rf v1.5/
```

> 进入`.julia/environments/v1.5`文件夹下
>
> 把`Manifest.toml`和`Project.toml`文件复制
>
> 再进入到`v1.6`文件夹下把`Manifest.toml`和`Project.toml`粘贴好
>
> 删除旧版本环境
>
> 删除旧版本的编译结果来节省存储空间
>
> 打开你的Julia

```shell
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.6.0 (2021-03-24)
 _/ |\__'_|_|_|\__'_|  |  Official https://julialang.org/ release
|__/                   |

(@v1.6) pkg>
```

__接下来就会自动多线程编译你曾经安装过的包了ヾ(≧∇≦*)ゝ__

__看着跑满的CPU,是不是很兴奋呢?ヾ(≧∇≦*)ゝ__



***

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。