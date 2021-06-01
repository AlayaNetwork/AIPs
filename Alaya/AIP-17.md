---
AIP: 17
Topic: Alaya网络优化升级提案
Author: alliswell
Status: Draft
Type: Text
Description: Alaya网络优化升级，修复已知问题
Created: 2021-05-28
---

# AIP-17：Alaya网络优化升级提案

## 目的

提议对Alaya底层节点网络进行升级，修复长期以来影响用户体验但一直未解决的问题。

## 新特性

无

## 优化功能

- 节点进程名由原来的 `platon` 修改为 `alaya`，启动命令中不再需要指定参数 `--alaya` 

- 优化交易传播策略，对于不直接广播交易的节点，发送交易hash值[#1780](https://github.com/PlatONnetwork/PlatON-Go/issues/1780)

- 支持RPC返回chainid的特性（参考EIP-695）

- alayakey工具优化，genblskeypair命令输出BlsProof

- 根据社区提议对Alaya网络随机性选举节点出块，累积二项分布函数期望值调整为30，[讨论](https://forum.latticex.foundation/t/topic/4119)

- 支持在创建网络时指定当前网络地址前缀`hrp`

   1. 支持在创世区块中指定hrp，hrp需符合bech32规范
   2. 网络初始化时，hrp会被记录到创世区块
   3. 除alaya主网外，其他chainid不绑定hrp， 避免因各个节点hrp设置不同导致其他问题
   4. hrp不指定时默认值为atp
   5. `platon account new / alayakey generate / alayakey generate` 命令支持传入hrp， 不传时默认使用atp
   6. alayakey 子命令updateaddress支持任意eip55或bech32地址转换为目标地址， 目标地址hrp需手动输入，不输入时使用默认值

## bug修复

- 对节点因零出块处罚锁定后，重新返回验证人时[总权重错误](https://github.com/PlatONnetwork/PlatON-Go/issues/1654)问题导致的错误节点信息进行修复
- 修复预估gas接口时，对于治理合约的预估，必须要传入gasPrice的问题[#1758](https://github.com/PlatONnetwork/PlatON-Go/issues/1758)
- 修复call调用偶现返回-32000错误码问题[#1769](https://github.com/PlatONnetwork/PlatON-Go/issues/1769)
- 修复创世块extra字段判断逻辑错误问题[#1757](https://github.com/PlatONnetwork/PlatON-Go/issues/1757)
- 修复节点选举随机性问题[issue-1785](https://github.com/PlatONnetwork/PlatON-Go/issues/1785)
- 修复节点fast同步失败后出现 `BAD BLOCK` 的问题[issue-1783](https://github.com/PlatONnetwork/PlatON-Go/issues/1783)
- 修复WASM跨合约调用时 `platon_caller` 值错误问题[issue-1779](https://github.com/PlatONnetwork/PlatON-Go/issues/1779)
- 修复因委托收益不能领取的bug[issue-1583](https://github.com/PlatONnetwork/PlatON-Go/issues/1583)导致的账目错误问题

## 说明

  本次升级将兼容历史数据，需要链上治理升级。详见讨论[链接](https://forum.latticex.foundation/t/topic/5070)

## 版本信息

本次升级的版本号为：0.16.0

Commit-ID: 待定

