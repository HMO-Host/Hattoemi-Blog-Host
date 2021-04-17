---
title: About Julia
date: 2020-08-21T10:32:30.000+08:00
tags:
- Julia

---
### 又一次开始

从Java的Spring到JavaFX，直到现在的Julia，经过了主流Web，到“过时”的GUI，直到现在的“万金油”Julia，因为繁琐，复杂，困难等〒▽〒，我已经从新来过了无数次o(≧口≦)o，在任何方面的。说实话，不疲惫是不可能的，这些年来的经验和教训，我希望能够通过博客的方式来告诉大家，同时也能够使我记得那些我曾经踩过的坑（甚至是黑洞━━∑(￣□￣*|||━━），作为一名女子高中生👍🏻

***

### 镇 楼

```julia
Julia Version 1.5.0
Commit 96786e22cc (2020-08-01 23:44 UTC)
Platform Info:
  OS: Linux (x86_64-pc-linux-gnu)
  CPU: Intel(R) Xeon(R) CPU           L5638  @ 2.00GHz
  WORD_SIZE: 64
  LIBM: libopenlibm
  LLVM: libLLVM-9.0.1 (ORCJIT, westmere)
Environment:
  JULIA_PKG_SERVER = https://mirrors.bfsu.edu.cn/julia
```

***

### 基础

<div staly="">
<div>
<img src="https://static.hdslb.com/player/images/ic_launcher.png" alt="bilibil" width="55" hight="55" /><a src="https://www.bilibili.com/video/BV1pK411T7he">夏季会议</a>
</div>
<div>
<img src="https://static.hdslb.com/player/images/ic_launcher.png" alt="bilibili" width="55" hight="55" /><a src="https://www.bilibili.com/video/BV1yt411c7Gm">基础教程</a>
</div>
<div>
<img src="https://cn.julialang.org/assets/infra/zhihu.svg" alt="zhihu" width="55" hight="55" /><a src="https://zhuanlan.zhihu.com/p/41802723">知乎</a>
</div>
<div>
<img src="https://cn.julialang.org/assets/infra/logo_cn.png" alt="cn" width="55" hight="55" /><a src="https://docs.juliacn.com/latest/">中文社区</a>
</div>
<div>
<img src="https://cn.julialang.org/assets/infra/discourse.svg" alt="discourse" width="55" hight="55" /><a src="https://discourse.juliacn.com/">中文论坛</a>
</div></div>

这些其实没什么好说的，你必须花时间去看，去认真学

## 坑（〒▽〒）（注：我用的是1.5.0版本，Julia自1.0.0版本后的变动很大）

### 新手

```julia
using Plots
```

然后就.................

```julia
ERROR: ArgumentError: Package Plots not found in current path:
- Run `import Pkg; Pkg.add("Plots")` to install the Plots package.

Stacktrace:
 [1] require(::Module, ::Symbol) at ./loading.jl:893
```

唉😕，那是因为没有安装这个包(packages)

```julia
# 按下"]"后输入add Plots
(@v1.5) pkg> add Plots
# 或者通过代码的组合(用";"来分隔，建议分号后加上空格)
julia> import Pkg; Pkg.add("Plots")
```

以后都可以通过这种(或者类似的)方式来安装[别的包](https://juliaobserver.com/)

tips:除了Plots，还有其它的绘图库，比如GR、PlotlyBase、Makie，我个人喜欢Makie，由纯Julia编写而成，它会使用GPU进行绘图，默认情况下使用[GLMakie.jl](https://github.com/JuliaPlots/GLMakie.jl),，当然还有其它子库，比如[CairoMakie.jl](https://github.com/JuliaPlots/CairoMakie.jl) 、[WGLMakie.jl](https://github.com/JuliaPlots/WGLMakie.jl) 、 [AbstractPlotting.jl](https://github.com/JuliaPlots/AbstractPlotting.jl)、[StatsMakie.jl](https://github.com/JuliaPlots/StatsMakie.jl) 、[StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl)，总而言之，非常强大，你甚至可以用它来创造一个小型的GUI程序。[这里](https://makie.juliaplots.org/stable/index.html)是Makie的官方文档

tips:如果你和我一样，喜欢制作桌面应用程序，你应该看一下[QML.jl](https://github.com/barche/QML.jl)和[Gtk.jl](https://github.com/JuliaGraphics/Gtk.jl)，尤其是[QML.jl](https://github.com/barche/QML.jl)，它可以和Makie联动

***

    为什么Julia运行这么慢，说好的“它要像C语言一般快速”呢？

你看......(展示前用过一次@time)

```julia
julia> @time using Makie
 16.955689 seconds (10.33 M allocations: 602.127 MiB, 1.02% gc time)
julia> @time using Makie
  1.820663 seconds (1.46 M allocations: 72.172 MiB)
julia> @time using Makie
  0.000163 seconds (320 allocations: 19.234 KiB)
```

所以为什么呢？

这是Julia的特性，别忘了它是动态语言，而且用的编译方式是JIT(Just in time)

这也是我喜欢Julia的原因，作为一门新的动态语言，它用的是JIT，同时保证了代码的简易性和高性能，毕竟编译(build)的速度和C差不多，即便我是从Java转过来的(还是搞GUI的)，Julia也能够满足我的需求。说实话，用的越久，你就越能感受到Julia的强大，觉得慢就多build一下吧，就当作是美中不足吧。[这里](https://discourse.juliacn.com/t/topic/312)有优化的建议，你也别乱build

tips:理智的时间\~除非你有需求，否则不建议使用Julia，它适合写小型项目，或者脚本，编译时间长是大家有目共睹的(虽然你可以丢到Codecov里面分析，Travis CI里面编译，Microsoft Azure里面装X)，除非你想为开源社区贡献一份力量，否则好好回去学主流语言。强大固然是强大，但是要驾驭这份强大，你就得比它强大(不是这个语言〒▽〒，谁打得过MIT的一群人啊w(ﾟДﾟ)w，这里的意思是要有足够的经验，就比如会Linux From Scratch之类的o(TヘTo) ，连拿[BinaryBuilder.jl](https://github.com/JuliaPackaging/BinaryBuilder.jl)去build[Yggdrasil](https://github.com/JuliaPackaging/Yggdrasil)需要的依赖都是划水<del>(虽然确实是划水)</del>)

tips:什么是"@time"?这是用来分析内存分配的，详情在[中文官方文档](https://docs.juliacn.com/latest/manual/profile/#%E5%86%85%E5%AD%98%E5%88%86%E9%85%8D%E5%88%86%E6%9E%90)里面有，还有其它强大的分析工具，多看看文档总没错👍🏻

***

    多线程?多进程?协程?（问号三连）

首先是多线程：(注：我关闭了Intel® HT，所以逻辑核心数与物理核心数相同，都是6个)

Linux/OSX下：

```shell
export JULIA_NUM_THREADS=6
```

Windows下：

```powershell
set JULIA_NUM_THREADS=6
```

这样我们就成功的设置好了Julia的线程数量，为6个，你们要根据自己的物理/逻辑核心数来设定线程数量哦～

接下来，验证一下

```julia
julia> Threads.nthreads() # 这里是输入，下面是输出
6
```

<del>关于怎么去用这些线程，在Julia官方文档里已经描述过了，在此不再赘述</del>

<del>可是我就要你赘述</del>

那么怎么去用这些线程呢?

***

    用什么IDE好呢？

来自官方的大家统一认为目前最好是GitHub Inc的Atom，其中的Juno插件非常好，而未来是VSCode，这同时也是我个人推荐的IDE，功能非常强大，最后推荐的是IDEA，理由在下面。

## 啊，真香

Atom的插件Juno

> 优点：
>
> * 会根据CPU核心数设置Julia的并发数，也就是自动多线程
> * 适配多种性能分析工具
> * 目前最受欢迎的JuliaIDE

> 缺点：
>
> * 啊，你看这国内的网速(一共要安装三个插件才能使用Juno，而且在国内的网下，很容易失败)
> * 容易出现莫名其妙的错误

VSCode的插件

(其实我感觉没什么可说的，估计这是最稳定的IDE了吧)

IDEA的插件

> 优点：
>
> * 对习惯使用Java的同志们比较友好，因为熟悉(尤其是像我这种双语言混搭的人)
> * 不错(也就只是不错)的代码提示

> 缺点：
>
> * 插件停止更新了
> * 只会include("xxx.jl")

tips:include("xxx.jl")这种加载方式在夏季会议中提到过，它能够加载一个.jl文件里面的所有代码

***

## 实战

\[PkgTemplates.jl\](https://github.com/invenia/PkgTemplates.jl)

---



***

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。