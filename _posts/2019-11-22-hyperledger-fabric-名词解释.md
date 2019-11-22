---
layout : post
title : hyperledger fabric 名词解释
date : 2019-11-22 12:53:37 +0800
categories : hyperledger fabric
description : hyperledger fabric 中文名词解释
---

# hyperledger fabric 名词解释

## 1 Block – 区块 

在⼀个通道上，区块是⼀组有序交易的集合。在通道中经过加密（哈希加密） 

后与前序区块连接。 

## 2 Chain – 链 

Zhu Jiang:账本的链是⼀个交易区块经过“哈希连接”结构化的交易⽇志。对等 

节点从排序服务收到交易区块，基于背书策略和并发冲突来标注区块的交易为 

有效或者⽆效状态，并且将区块追加到对等节点⽂件系统的哈希链中。 

## 3 节点 

### 3.1 Committer – 提交节点 

1.0 架构中⼀种 peer 节点⻆⾊，负责维护区块链和账本结构。对 orderer 排序 

后的交易进⾏检查（包括交易消息结构、签名完整性、是否重复、读写集合版 

本是否匹配等），检查完成后选择合法的交易执⾏并写⼊存储。 

同⼀个物理节点可以仅作为Committer⻆⾊运⾏，也可以同时担任Endorser和 

Committer这两种⻆⾊。 

### 3.2 Endorser – 背书节点 

1.0 架构中⼀种 peer 节点⻆⾊，负责检验某个交易是否合法，是否愿意为之背 

书、签名。 

收到来⾃客户端的交易提案后，⾸先进⾏合法性和ACL权限检查，检查通过则 

模拟运⾏交易，对交易导致的状态变化（以读写集形式记录，包括所读状态的 

键和版本，所写状态的键值）进⾏背书并返回结果给客户端。注意⽹络中可以 

只有部分节点担任Endorser⻆⾊。 

### 3.3 Orderer – 排序节点

1.0 架构中的共识服务⻆⾊，为⽹络中所有合法交易进⾏全局排序，并将⼀批 

排序后的交易组合⽣成区块结构。 

⽬前Orderer⽀持Solo（单节点共识）、kafka（分布式队列）、PBFT（拜占庭 

容错）三种模式。 

#### 3.3.1 Solo – 单节点共识 

order-solo模式作为单节点通信模式，所有从peer收到的消息都在本节点进⾏ 

排序与⽣成数据块，因此不需要“共识”；对应的也就失去了⾼可⽤性与拓展 

性。Solo使得开发与测试⾮常的简便易于使⽤，这种模式主要是为了⾮⽣产环 

境⽽存在的。 

#### 3.3.2 kafka – 分布式队列 

此模式需要加⼊⼀个kafka集群统⼀分配处理所有Orderer的数据。Orderer服务 

从kafka集群⾥获取相应topic，即在kafka队列中隔离出来不同的作⽤域供 

Orderer使⽤。kafka的分布式⼀致机制确保了我们的交易数据是有序的。 

虽然引⼊了kafka带来了较⾼的吞吐量以及可⽤性，但是却没有拜占庭容错。 

#### 3.3.3 PBFT – 拜占庭容错

### 3.4 Peer – 节点 

⼀个⽹络实体，维护账本并运⾏链码容器来对账本执⾏读写操作。peer由 

Member拥有和维护。 

### 3.5 Leading Peer – 主导节点 

每⼀个Member在其订阅的channel上可以拥有多个peer，其中⼀个peer会作为 

channel的leading peer代表该Member与ordering service通信。ordering 

service将block传递给leading peer，该peer再将此block分发给同⼀member下 

的其他peer。 

## 4 Chaincode – 链码 

即智能合约，是⼀个运⾏在账本上的⼀段代码，⽤来实现不同的业务逻辑，可 

以实现对StateDB的增删改查。 

⽀持golang等开发语⾔，运⾏在独⽴的Docker环境中。从Fabric1.0开始 

Chaincode⽀持更新部署。 

## 5 Channel – 通道 

通道是构建在“Fabric”⽹络上的私有区块链，实现了数据的隔离和保密。通道 

特定的账本在通道中是与所有对等节点共享的，并且交易⽅必须通过该通道的 

正确验证才能与账本进⾏交互。通道是由⼀个“配置块”来定义的。 