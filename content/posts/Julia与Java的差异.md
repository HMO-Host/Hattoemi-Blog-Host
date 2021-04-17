---
title: Julia与Java的差异
date: 2020-08-21T10:32:30.000+08:00
tags: 
- Julia
- Java

---

# Julia与Java的差异

> 一个是动态语言另一个是静态语言之类的话就不说了,这里主要讨论的是实际使用时(尤其是算法学习过程中)两语言的不同之处
>
> 看到"尤其是算法学习过程中"这句话就退出的同学们,不要以为大多数是关于算法的内容就一定与你们的需求无关了,况且我还有别的呐!
>
> 注:
>
> * 只是想要选择学习哪一种语言的小伙伴们不要看了(ノへ￣、),这里没有你们需要的,再者,Julia的入门难度不是盖的
> * 这里只说差异,不评论优缺点
> * 这里只是记录我在学习过程中遇到的问题,我不敢说自己熟悉Julia,而且我的观点也不一定是成熟的o(TヘTo),若有疏漏,还请多多指教
> * 目前以下的知识点还没有经过整理,几乎是想到什么就写什么

### 接口

这是一个Node（～￣▽￣～） 

Java的写法

```java
public class Node implements Comparable<Node>{
    int weight;
    byte data;
    Node left;
    Node right;

    public Node(Byte data, int weight) {
        this.data = data;
        this.weight = weight;
    }

    @Override
    public int compareTo(Node o) {
        return o.weight-this.weight;
    }

    @Override
    public String toString() {
        return "Node{" +
                "weight=" + weight +
                ", data=" + data +
                '}';
    }
}
```

大家基本上都是这么写的对吧（～￣▽￣～） 

通过 `implements` 关键字接入并实现接口,让`Node`可以被迭代

而这是Julia的写法

```julia
struct Node
	weight::Int
	byte::UInt8
	left::Node
	right::Node
end

# 熟练或者听取意见认真阅读文档的同学可能已经发现了问题
Base.iterate(N::Node, state=1) = state > N.weight ? nothing : (state, state-1)
```

现在它"看起来"可以被迭代了

这个时候肯定有同学要闻

`Base.iterate(N::Node, state=1) = state > N.weight ? nothing : (state, state-1)`这一行代码是个啥子意思勒?"

__耐心的跟旅同学走一套正常流程哟～__

首先是`Base.iterate`这是Base模块下的`iterate`方法,一起跑去看文档

唉!你往哪里跑呀?这里这里!别划水去了鸭

> 除了在浏览器上搜索并查看官方文档,还有一个比较快捷的方法
>
> 1. 打开终端,进入Julia
> 2. 按下`?`键
> 3. REPL变成黄色的`help?> `之后
> 4. 输入你想要搜索的Function

文档是这么描述`iterate`哒(注:中文是我自己翻译的,实际文档里并没有中文注释)

```julia
iterate(iter [, state]) -> Union{Nothing, Tuple{Any, Any}}

  Advance the iterator to obtain the next element. If no elements remain,
  nothing should be returned. Otherwise, a 2-tuple of the next element and the
  new iteration state should be returned.
  迭代迭代器以获取下一个元素。如果没有剩余元素，则不应返回任何内容
  否则，应该返回下一个元素的2元组和新的迭代状态

  ────────────────────────────────────────────────────────────────────────────

  iterate(s::AbstractString, i::Integer) -> Union{Tuple{<:AbstractChar, Int}, Nothing}

  Return a tuple of the character in s at index i with the index of the start
  of the following character in s. This is the key method that allows strings
  to be iterated, yielding a sequences of characters. If i is out of bounds in
  s then a bounds error is raised. The iterate function, as part of the
  iteration protocol may assume that i is the start of a character in s.
  在索引i处返回s中字符的元组，索引位于s中的下一个字符的开头
  这是允许对字符串进行迭代的关键方法，以此来生成字符序列
  如果i在s中超出界限，则引发界限错误
  作为迭代协议的一部分，iterate函数可以假设i是s中字符的开始

  See also: getindex, checkbounds
```

现在你看不懂很正常,以后也不一定看得懂ᕕ( ᐛ )ᕗ

> 以下改自中文官方文档,由于使用的是文档中描述的第一个方法,这里也只说明第一个方法

```julia
iterate(iter, state)
```

通常返回由下一项及其状态组成的元组，或者在没有下一项存在时返回 [`nothing`](https://docs.juliacn.com/latest/base/constants/#Core.nothing)。

顺序迭代由 [`iterate`](https://docs.juliacn.com/latest/base/collections/#Base.iterate) 函数实现。 Julia 的迭代器可以从对象外部跟踪迭代状态，而不是在迭代过程中改变对象本身。 迭代过程中的返回一个包含了当前迭代值及其状态的元组，或者在没有元素存在的情况下返回 `nothing`。 状态对象将在下一次迭代时传递回 iterate 函数，并且通常被认为是可迭代对象的私有实现细节。

任何定义了这个函数的对象都是可迭代的，并且可以被应用到[许多依赖迭代的函数上](https://docs.juliacn.com/latest/base/collections/#lib-collections-iteration) 。 也可以直接被应用到  [`for`](https://docs.juliacn.com/latest/base/base/#for) 循环中

现在懂了的同学举个手,没懂的同学不要灰心,这部分内容其实可以稍微跳过

接下来肯定又有同学要问了

"那么`=`后面的代码是啥子意思勒?"

熟悉C/C++的同学一定不陌生,没错,是`三元表达式`(也有其它叫法,不过一般指的是这一个)

它的意思大概是这样的:

> state 大于 N.weight 吗? 如果不是,那就啥也不干(`nothing`),如果是,那就丢个`(state, state-1)`

有点像`for`循环,不是吗?但它在C/C++程序中是一种优化的写法,如果具有一定顺序,那么通过CPU预判,一般可以提升约20%的性能

Julia里面任何循环都是有优化的,你随便写(大概)

它看起来将是逆序迭代的

接下来我们验证一下

```julia
 for i in Squares(7)
     println(i)
 end
```

Ops!就算程序没有停下,你也知道这不是你想要的(☄⊙ω⊙)☄

> 以下摘自中文官方文档

能以*逆序*迭代集合也很有用，这可由 [`Iterators.reverse(iterator)`](https://docs.juliacn.com/latest/base/iterators/#Base.Iterators.reverse) 迭代实现。但是，为了实际支持逆序迭代，迭代器类型 `T` 需要为 `Iterators.Reverse{T}` 实现 `iterate`。（给定 `r::Iterators.Reverse{T}`，类型 `T` 的底层迭代器是 `r.itr`。）在我们的 `Squares` 示例中，我们可以实现 `Iterators.Reverse{Squares}` 方法：

```julia
julia> Base.iterate(rS::Iterators.Reverse{Squares}, state=rS.itr.count) = state < 1 ? nothing : (state*state, state-1)

julia> collect(Iterators.reverse(Squares(4)))
4-element Array{Int64,1}:
 16
  9
  4
  1
```

那么代入我们的代码中应该怎么做呢?

```julia
Base.iterate(rS::Iterators.Reverse{Node}, state=rS.itr.weight) = state < 1 ? nothing : (state, state-1)
```

"那么,我终于可以用它了?"

虽然我没有测试,但是应该是没有问题了

"( ‵▽′)ψ淦,这么麻烦,不学了!"

别啊（～￣▽￣～）,要迎难而上

为什么会出现这样的情况呢?

因为Julia并不是面对对象的,因此这个"接口"并不是真正意义上的接口,而是伪接口

但这样也不会在你打算使用(实现)其它接口时会出现困难,只要你会写接口

"谢谢,学废了"

啊啊啊!别走啊......这样的情况你将会遇见很多次,但是就此放弃的话我也建议你不要学习下去了,这也是中国社区的一致态度

不要认为我们态度恶劣,而是Julia本身就不适合畏难的人学习,而且这样的人到哪里都不被欢迎

因此,请务必坚持下去,这是对当初作出选择的你的答复

你有为之献上一切的觉悟吗?

(这才第一个呐〒▽〒内牛满面了)

### 设计模式

作为动态语言,能够预编译和编译动态链接库已经很不错了,你还想要设计模式,真是

__欲～ 求～ 不～ 满～ 啊～__



***

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。