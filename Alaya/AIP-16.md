---
AIP: 16
Topic: 兼容以太坊
Author: clearly
Status: Draft 
Type: Text
Description: 底层全面兼容以太坊的生态
Created: 2021-05-28
---

# AIP-16：关于全面兼容以太坊

## 摘要
为吸引更多开发者参与 Alaya 网络中来，降低开发者将 Dapp 应用从以太坊迁移到 Alaya 上的开发成本，Alaya 应该在如 SDK、EVM、RPC 接口、solidity 语言等方面兼容以太坊。

## 动机

以太坊作为世界上第二大市值的区块链网络，也是最大的智能合约平台，有着众多的开发者和成熟的社区，许多开发者是通过以太坊和他们的智能合约进入区块链世界的，他们对使用以太坊智能合约以及与开发 Dapp 相关的工具、SDK 等都很熟练，但对 Alaya 不熟悉，因此如果能在 Dapp 开发层面实现对以太坊的兼容，无疑将很大程度上提升 Alaya 对开发者的吸引力，生态也会逐渐壮大起来。

当前 Alaya 和以太坊不兼容的地方:

- 地址格式不同，Alaya 采用 bech32 的地址格式，以太坊采用的是 EIP55 的地址格式
- Token 单位不同，Alaya 的 Token 单位为 atp/von，以太坊的为 ether/wei
- 部分函数在 Alaya 中没有实现或者实现不同。如 block.difficulty、miner.setEtherbase 等函数，使用到这些函数的以太坊合约可能不适合在 Alaya 上运行，需要进行相应调整，不过这些函数很少使用
- 区块头时间戳不同，以太网为秒，Alaya 为毫秒

由以上差异可知，Alaya 只需要极小的改动就可以实现对以太坊的兼容。

## 实现说明

### RPC 接口兼容

#### 1. 接口格式兼容
扩展 JSON-RPC 2.0，对 request 请求对象做出以下修改:  
 - 增加 bech32 字段，Booleans 类型。bech32 为 true 表示此次 rpc 调用中地址部分的编解码格式为 bech32，默认为 EIP55。
 - 优化 method 字段，在命名空间中增加对 eth 的支持，eth 等同于 platon。

接收 request 的流程做如下优化：
1. 优先通过 method 中是否包含 eth/platon 来区分是以太坊 /alaya 调用
    ```
    // Alaya 调用
    curl -X POST --data '{"jsonrpc":"2.0","method":"platon_getBalance","params":["atp1zqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqp8h9fxw", "latest"],"id":1}'
    // 以太坊调用
    curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1", "latest"],"id":1}'
    ```
2. 如果 method 相同，通过 request 中 bech32 的值来区分是以太坊 /alaya 调用
    ```
    // Alaya 调用
    curl -X POST --data '{"jsonrpc":"2.0","bech32":true, "method": "txpool_contents", "params": [], "id": 1}'
    // 以太坊调用
    curl -X POST --data '{"jsonrpc":"2.0", "method": "txpool_contents", "params": [], "id": 1}'
    ```

对于来自以太坊的调用的响应对象，地址的编解码格式为 EIP55。对于来自 alaya 的调用的响应对象，地址的编解码格式为 bech32。示例:
```
 // Alaya 调用
 {"jsonrpc":"2.0","id":1,"result":["atp1zqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqp8h9fxw"]}
 // 以太坊调用
 {"jsonrpc":"2.0","id":1,"result":["0x407d73d8a49eeb85d32cf465507dd71d507100c1"]}
```

#### 2. 需要新增或修改的接口
以太坊中的一些 RPC 接口 Alaya 中没有或实现不同，我们需要对此进行适配。

1. miner.setEtherbase
因为 Alaya 中区块提议人都已明确制定固定的收益地址，因此 miner.setEtherbase 接口无需在 Alaya 中实现。

### solidity 合约兼容

#### 1. 底层指令兼容
经排查，EVM 底层指令 Alaya 和以太坊已经基本兼容，不兼容的指令有:
- TIMESTAMP
  Alaya 返回的是单位是 ms，以太坊返回的单位是 s. 该指令的返回单位需要统一改为 s。

#### 2. 编译器兼容

编译器兼容以太坊主要体现在 solidity 合约中的地址格式，当前 Alaya 的合约编译器只支持 bech32 个，为实现对以太坊合约的兼容，只需在每个 solidity 大版本的最新版 (0.4.26，0.5.17，0.6.12，0.7.6 和 0.8.4）实现对 EIP55 地址格式的兼容即可。

对于 Token 单位来说，为提示用户或开发者当前是在 Alaya 网络中使用合约，因此不建议对以太坊 Token 单位 `ether/wei` 实现兼容。

## 说明
本次升级将兼容历史数据，需链上治理升级。详见讨论 [链接](https://forum.latticex.foundation/t/topic/4636)

