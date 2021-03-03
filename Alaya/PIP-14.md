---
PIP:  14
Topic: Alaya网络优化升级提案
Author: alliswell
Status: Final 
Type: Upgrade
Description: 关于支持同时使用锁仓和自有Token进行质押功能以及一些其他的优化
Created: 2021-01-25
---

# PIP-14：Alaya版本升级-0.15.0

## 目的

当前Alaya网络中各个验证人节点多是使用锁仓计划中的Token进行质押成为验证节点，由于当前版本质押时只支持使用一种类型的Token，导致用户在实际使用的过程中遇到诸多问题，本次升级也是充分听取用户的改进建议，支持在质押时同时使用两种类型的Token。除此之外，本次升级还针对选举验证人的二项分布算法等做了优化调整。

## 新特性

- 质押支持同时使用两种金额

  对质押交易中的类型(typ)字段，用户可以指定为：
  0 表示使用自有金额
  1 表示使用锁仓余额
  2 优先使用锁仓余额，锁仓余额不足则剩下的部分使用自有金额
  此优化解决了用户自有余额和锁仓余额都无法发起质押，但两种金额之和满足最低质押限制却不能使用的问题。

- 根据质押总量动态调整二项分布参数

  根据质押总量的变化动态调整选举验证人时的二项分布的参数，以保证选举过程中各个验证人被选中的概率曲线更平滑。
  
- 低版本节点在链升级通过后主动退出
  
  治理升级提案已经获得通过的前提下，旧版本已不能继续运行，如果不主动退出运行将导致节点在分叉区块持续执行区块失败（bad block）进而不断请求从邻居节点同步区块，导致邻居节点网络流量无谓增加。

## 优化功能

- 优化当前验证节点p2p连接规则，减少不必要的流量损耗

  由于部分未升级的节点没有及时退出运行，导致网络流量暴增，为避免不必要的流量开销，本次升级做如下优化：
  
  1. 对当前网络已升级的验证人节点记录到白名单（快照时间为2021-1-7）
  
  2. 将握手协议版本号升级到6
  
  3. 当新节点收到满足以上任意条件的连接请求将获准建立连接，否则连接将被拒绝

- 内置合约错误描述信息翻译矫正

  矫正了部分内置合约交易的错误提示信息。
  
- 去掉txpool.pricelimit参数

  因Alaya节点不区分miner和非miner，故去掉此参数。
  
## bug修复

- 对0.14.0之前版本由于[锁仓问题](https://github.com/PlatONnetwork/PlatON-Go/issues/1625)导致的坏账进行平账处理

- 修复对零出块处罚中的节点解委托时[权重未调整](https://github.com/PlatONnetwork/PlatON-Go/issues/1654)的问题

- 修复节点[零出块被处罚后回到验证人列表需要重新声明版本号](https://github.com/PlatONnetwork/PlatON-Go/issues/1666)问题

## 说明

  本次升级将兼容历史数据，需要链上治理升级。详见讨论[链接](https://forum.latticex.foundation/t/topic/4107)

## 版本信息

本次升级的版本号为：0.15.0

Commit-ID: 9867ee6809041f33ec0580589290d9eddac6a971
