---
title: Huffman编码
date: 2021-02-11T11:59:30.000+08:00
tags: 
- Algorithm learning from scratch
---

# Huffman编码

> __以下改自维基百科__,由于翻译可能具有歧义(如赫夫曼,哈夫曼,霍夫曼等),这里只写作Huffman
>
> - 在计算机资料处理中,Huffman编码使用变长编码表对源符号(如文件中的一个字母)进行编码,其中变长编码表是通过一种评估来源符号出现几率的方法得到的,__出现几率高的字母使用较短的编码,反之出现几率低的则使用较长的编码__,这便使编码之后字符串的平均长度、期望值降低，从而达到无损压缩数据的目的
> - Huffman树又称最优二叉树，是一种__带权路径__长度最短的二叉树。所谓树的带权路径长度,就是树中所有的叶节点的权值乘上其到根节点的路径长度(若根节点为0层,叶节点到根节点的路径长度为叶节点的层数)。树的路径长度是从树根到每一节点的路径长度之和,记为WPL = (W1 x L1 + W2 x L2 + W3 x L3 + Wn x Ln),N个权值Wi(i = 1, 2, ...n)构成一颗有N个节点的二叉树,相应的叶节点的路径长度为Li(i = 1, 2, ...n)。可以证明Huffman树的WPL是最小的

__对不起哈,因为我使用的是Ubuntu,没有什么特别好的绘图方式(主要是没有数位板),而且个人Julia绘图技术并不是特别好,各位同学们就凑合凑合__

然后就是我Julia在这方面并不是很上手,没有什么余裕

首先我们有了一个叫做Node的对象(struct)

![Node](../../../../图片/Node.png)

#### Julia实现

> 思路会很像Java而不是Julia

```julia
# 可变类型
mutable struct Node
	# 说明这必须是Node类型
    left::Node
    right::Node
    weight::Int
    # 也就是byte
    data::UInt8

    function toString()
        return "Node{'
            weight = $weight
            , data = $data
            '}"
    end
end
```

#### Java实现

```java
package demo;

/**
 * 继承`Comparable`接口使Node可以被迭代
 * @author hattoemi
 */
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

这个Node具有

- `wegiht` 权值
- `data` 数据
- `left` 左节点
- `right` 右节点

__那这个Node是拿来干什么的亚?__

所谓`Node`就是__二叉树__的节点

__哇!系二叉树,溜了溜了__

不要怕啊,二叉树就是一个

![二叉树](../../../../图片/二叉树.png)

<del>Julia?</del>

__好了回归正题,接下来我们把Huffman压缩的实现思路梳理一遍__

1. 获取节点
2. 创建树
3. 获取编码表
4. 返回数据和编码表

### 获取节点

#### Julia实现

```julia
function getCodes(tree::Node)
    if tree === nothing
        error("你搁这整活呐?")
    end
    getCodes(tree.left, "0")
    getCodes(tree.right, "1")
    return huffmanCodes
end

function getCodes(node::Node, code::String)
    str = Array{String, 1}
    push!(str, code)
    if node.data === nothing
        getCodes(node.left, "0")
        getCodes(node.right, "1")
    else
        push!(huffmanCodes, node.data, str)
    end
end
```


***

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。