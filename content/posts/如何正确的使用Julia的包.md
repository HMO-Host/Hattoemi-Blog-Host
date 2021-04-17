---
title: 如何正确的使用Julia的包
date: 2021-02-13T11:59:30.000+08:00
tags: 
- Julia
---

> 当我们需要引入一些不在Julia注册表里的包/自己新建文件夹而不是使用`generate`或者通过`PkgTemplates.jl`创建的包时,我们该如何将其添加到Julia的环境呢?

### 不在Julia注册表里的包

1. 第一种情况,GitHub上有的项目
2. 第二种情况,GitHub上无法引入的项目

#### GitHub上有的项目

[__给我好好看文档!__](https://docs.juliacn.com/latest/stdlib/Pkg/#%E6%B7%BB%E5%8A%A0%E6%9C%AA%E6%B3%A8%E5%86%8C%E5%8C%85)

```julia
pkg> add https://github.com/fredrikekre/ImportMacros.jl
```

1. 进入REPL(就是用终端打开的Julia界面)
2. 按下`]`
3. 输入`add`,按下`空格键`
4. 打开浏览器,在GitHub的项目页面里点击绿色的`Code`
5. 复制`https`链接
6. 回到REPL,按下`Ctrl+Shift+v`
7. 回车

#### GitHub上无法引入的项目

一般情况下,主要是因为这个包基于早期的Julia构建的

早期的Julia没有`Project.toml`这样的文件,具体详情在[这里](https://docs.juliacn.com/latest/stdlib/Pkg/#%E8%AF%8D%E6%B1%87%E8%A1%A8)

解决方案1:

1. 在你的工作目录(或者你喜欢的文件夹下)打开Julia
2. 进入`pkg>`模式
3. 输入`generate 项目名称`
4. 将除了`Project.toml`文件以外的所有文件与文件夹删除,并替换成你clone下来的文件
5. 回到终端,输入`activate .`,__注意,activate后面有空格__
6. 输入`up; precompile`(如果是1.6版本,可以只输入`instantiate`,这样相对简单一些)

如果你不打算提交更改以让这个包适应新版本Julia而只是自用的话,这个方法相对方便一些

__其中,你可以仅仅移动`Project.toml`文件并进行其它操作达到同样的效果,但是考虑到看这篇文章的读者水平可能有很大不同,这里写了适合爱抄代码的小白能够接受的教程__

解决方案2:

1. 使用`PkgTemplates.jl`构建一个同名项目
2. __删除原项目的`.git`文件夹__并将使用`PkgTemplates.jl`构建的项目的文件全部替换为原项目的

如果打算进行PR,这是个好选择

__注意,只进行这几步相当于私有化这个包,请查看原项目是否有开源协议并详细阅读,否则请修改使用`PkgTemplates.jl`时的参数,或者删除使用`PkgTemplates.jl`构建的项目的`.git`文件夹__

### 添加没有使用`generate`或者通过`PkgTemplates.jl`创建的包

你相当于创建了一个"GitHub上无法引入的包"

### `gc`与`dev`

[dev](https://docs.juliacn.com/latest/stdlib/Pkg/#%E5%BC%80%E5%8F%91%E5%8C%85):一种更加方便的添加到环境的方式

[gc](https://docs.juliacn.com/latest/stdlib/Pkg/#%E5%9E%83%E5%9C%BE%E6%94%B6%E9%9B%86%E6%97%A7%E7%9A%84%E3%80%81%E4%B8%8D%E5%86%8D%E4%BD%BF%E7%94%A8%E7%9A%84%E5%8C%85):减少磁盘占用



***

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。