# Multichain-BSC-Dashboard
Maybe nothing.

# 路由桥概述

路由分为2个主流币，2个原生币，1个山寨币

### 原生币桥

合约地址：0x92c079d3155c2722dbf7e65017a5baf9cd15561c

Dune接口：
```
select * from multichain_router."AnyswapV6Router_Native_Coin1_evt_LogAnySwapIn"

select * from multichain_router."AnyswapV6Router_Native_Coin1_evt_LogAnySwapOut"
```

合约地址：0xf9736ec3926703e85c843fc972bd89a7f8e827c0

Dune接口：
```
select * from  mutchain_route."AnyswapV3Router_Native_Coin2_evt_LogAnySwapIn"

select * from  mutchain_route."AnyswapV3Router_Native_Coin2_evt_LogAnySwapOut"
```

### 主流币桥：

0xd1C5966f9F5Ee6881Ff6b261BBeDa45972B1B5f3 ****
```
select * from multichain_router."**AnyswapV4Router_Mainstream_Coin1**_evt_LogAnySwapIn"

select * from multichain_router."**AnyswapV4Router_Mainstream_Coin1**_evt_LogAnySwapOut"
```

0xe1d592c3322f1f714ca11f05b6bc0efef1907859

### 山寨币桥:

0xABd380327Fe66724FFDa91A87c772FB8D00bE488

select * from multichain_v3."AnyswapV4Router_evt_LogAnySwapIn”

select * from multichain_v3."AnyswapV4Router_evt_LogAnySwapOut”

## 主流币桥:

1. 0xd1c5966f9f5ee6881ff6b261bbeda45972b1b5f3
2. 0xe1d592c3322f1f714ca11f05b6bc0efef1907859

0x533e（ETH→BSC桥）

从以太坊分析BSC桥（2.0的桥）

## 接口ABI：

![截屏2022-05-18 12.04.22.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/293e85a3-6361-4d43-90ce-c676b8457d21/截屏2022-05-18_12.04.22.png)

## 一些研究中发现的细节

跨链桥中From和To都可以为自身，表示为跨链自身钱包账户中，尤其是EVM兼容的链，地址相同

但也可以通过跨链的方式发送给其他钱包地址，因此**在计算用户数时候，使用To作为因子计算更为准确。**

参考案例：

1.跨链到自身钱包

[https://bscscan.com/tx/0x065c46071b9ec02570c30460e661c189745664b4b8de9f2f54a18501966a81bf#eventlog](https://bscscan.com/tx/0x065c46071b9ec02570c30460e661c189745664b4b8de9f2f54a18501966a81bf#eventlog)

2.跨链到另外一个钱包

[https://bscscan.com/tx/0xdba5484c3e323050bc7d8dbf20e415a4c326661214024e9900983e5409495e3a#eventlog](https://bscscan.com/tx/0xdba5484c3e323050bc7d8dbf20e415a4c326661214024e9900983e5409495e3a#eventlog)
