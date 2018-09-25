---
layout:     post
title:      "区块链一些相关概念的记录"
date:       2018-05-17 10:47:00
categories: Computer
tags:   ๑BlockChain
---

> 不适合人类阅读的学习笔记

## 一些主要的平台
---

- 比特币

- [以太坊](https://ethereum.org/) (**需要翻墙**)

- fabric

- [EOS](https://eos.io/)

## 一些概念
---

- 智能合约：智能合约是1994年由密码学家尼克萨博（Nick Szabo）首次提出的理念，几乎与互联网同龄。**智能合约是指能够自动执行合约条款的计算机程序**，在比特币出现以前，因为不存在安全可靠的执行环境，智能合约一直不能够应用到现实中。区块链由于其去中心化、公开透明等特性，天生就可以为智能合约提供可信的执行环境。所以，新型的区块链框架几乎都会内置智能合约的功能。

- 图灵完备：图灵完备性(Turing Compeleteness)是指针对一套数据操作规则而言的概念。数据操作规则可以是一门编程语言，也可以是计算机里具体实现了的指令集。当这套规则可以实现图灵机模型里的全部功能时，就称他具有图灵完备性。——[参考](https://www.zhihu.com/question/20115374)

> 简单来说，对于任何一个可以由计算解决的问题都能解决的编程语言或者是虚拟机称为是图灵完备的

### 共识算法

- POW(proof-of-work)：
> 工作量证明机制。工作量证明同时也是一种代币分发机制，它通过经济激励的方式来鼓励节点参与区块的构造过程，节点在构造区块的时候需要穷举一个随机数以使得区块符合规定的难度要求，一旦区块链出现分叉，诚实的节点将选择工作量较大的链条，而抛弃工作量较小的。由于假设所有节点都是逐利的，而选择工作量较小的链条就会使自己获得的激励无效，所以最终所有的节点都会是诚实的，从而使每个节点的区块链数据都保持一致。

- BFT(Byzantine Fault Tolerance):
> 拜占庭容错模型的共识机制。节点被分为普通节点和记账节点（Validating Peer），只有记账节点才会参与到区块的构造过程，这种角色的分离使得算法的设计者有机会将运行共识算法的节点数量限定在一个可控的规模内。

- PBFT(Practical Byzantine Fault Tolerance)：
> 实用拜占庭容错算法。PBFT是一种状态机副本复制算法，即服务作为状态机进行建模，状态机在分布式系统的不同节点进行副本复制。每个状态机的副本都保存了服务的状态，同时也实现了服务的操作。将所有的副本组成的集合使用大写字母R表示，使用0到`|R|-1`的整数表示每一个副本。为了描述方便，假设`|R|=3f+1`，这里f是有可能失效的副本的最大个数。尽管可以存在多于3f+1个副本，但是额外的副本除了降低性能之外不能提高可靠性。

- POS(Proof of Stake)：
> 股权证明。类似于财产储存在银行，这种模式会根据你持有数字货币的量和时间，分配给你相应的利息。 简单来说，就是一个根据你持有货币的量和时间，给你发利息的一个制度，在股权证明POS模式下，有一个名词叫币龄，每个币每天产生1币龄，比如你持有100个币，总共持有了30天，那么，此时你的币龄就为3000，这个时候，如果你发现了一个POS区块，你的币龄就会被清空为0。你每被清空365币龄，你将会从区块中获得0.05个币的利息(假定利息可理解为年利率5%)，那么在这个案例中，利息 = 3000 * 5% / 365 = 0.41个币，这下就很有意思了，持币有利息。

- DPOS(Delegated Proof of Stake)：
> 委任权益证明。股份授权证明机制（又称受托人机制），它的原理是让每一个持有比特股的人进行投票，由此产生101位代表 , 我们可以将其理解为101个超级节点或者矿池，而这101个超级节点彼此的权利是完全相等的。从某种角度来看，DPOS有点像是议会制度或人民代表大会制度。如果代表不能履行他们的职责（当轮到他们时，没能生成区块），他们会被除名，网络会选出新的超级节点来取代他们。DPOS的出现最主要还是因为矿机的产生，大量的算力在不了解也不关心比特币的人身上，类似演唱会的黄牛，大量囤票而丝毫不关心演唱会的内容。

- 石墨烯技术：
> 石墨烯技术是新一代的区块链技术，基于DPOS共识算法。目前市场上流行的区块链阵营有三种，一种是第一代以比特币为主的生态体系，他们是基于POW共识，纯粹的去中心化，基于p2p的加密数字货币技术；第二种就是以以太坊构成的生态体系，主要以基于智能合约的ERC20的代币体系，他们是基于POW共识，目前以太坊正准备切换到POW+POS的多共识体系；第三种就是进化到目前最强劲的石墨烯技术生态体系，它是基于DPOS（股份授权证明共识），支持高并发，高性能等大规模工业级商业场景的基础设施，诞生了BTS（BitShare）开源商业系统，Steem去中心化社交网络平台以及EOS。特点：转账速度特别快，吞吐量tps极高，安全性很高，没有原生bug出现，功能强大，应用性极高。


### 其他

- WebAssembly：
> WebAssembly(缩写Wasm)是一种基于堆栈的虚拟机的二进制指令格式。Wasm设计作为一个便携式的针对高级语言的编译器，例如C/C++/Rust，使各种客户端或服务端应用程序都能够在web中部署。

- TPS(transaction per second)：
> 服务器每秒处理的事务数。TPS包括一条消息入和一条消息出，加上一次用户数据库访问。（业务TPS = CAPS × 每个呼叫平均TPS）TPS是软件测试结果的测量单位。一个事务是指一个客户机向服务器发送请求然后服务器做出反应的过程。客户机在发送请求时开始计时，收到服务器响应后结束计时，以此来计算使用的时间和完成的事务个数。一般的，评价系统性能均以每秒钟完成的技术交易的数量来衡量。系统整体处理能力取决于处理能力最低模块的TPS值。

- QPS(quary per second)：
> 每秒查询率QPS是对一个特定的查询服务器在规定时间内所处理流量多少的衡量标准，在因特网上，作为域名系统服务器的机器的性能经常用每秒查询率来衡量。
对应fetches/sec，即每秒的响应请求数，也即是最大吞吐能力。



<br>
- 一些参考文章：[比特币、以太坊、Fabric…你知道它们的优缺点吗？](https://blog.csdn.net/Blockchain_lemon/article/details/79236199)、
[区块链3.0：拥抱EOS](https://www.cnblogs.com/Evsward/p/eos-intro.html)

<br>
> 最后更新于2018.5.17