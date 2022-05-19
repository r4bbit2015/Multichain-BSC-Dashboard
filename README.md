# Multichain-BSC-Dashboard
Maybe nothing.

# 路由桥概述

路由分为2个主流币，2个原生币，1个山寨币

### 原生币桥
(1) 合约地址：0x92c079d3155c2722dbf7e65017a5baf9cd15561c
```sql
select * from multichain_router."AnyswapV6Router_Native_Coin1_evt_LogAnySwapIn"
select * from multichain_router."AnyswapV6Router_Native_Coin1_evt_LogAnySwapOut"
```
(2) 合约地址：0xf9736ec3926703e85c843fc972bd89a7f8e827c0
```sql
select * from  mutchain_route."AnyswapV3Router_Native_Coin2_evt_LogAnySwapIn"
select * from  mutchain_route."AnyswapV3Router_Native_Coin2_evt_LogAnySwapOut"
```

### 主流币桥：
(1) 合约地址：0xd1C5966f9F5Ee6881Ff6b261BBeDa45972B1B5f3
```sql
select * from multichain_router."**AnyswapV4Router_Mainstream_Coin1_evt_LogAnySwapIn"
select * from multichain_router."**AnyswapV4Router_Mainstream_Coin1_evt_LogAnySwapOut"
```
(2) 合约地址：0xe1d592c3322f1f714ca11f05b6bc0efef1907859
```sql
select * from multichain_router."**AnyswapV4Router_Mainstream_Coin2_evt_LogAnySwapIn"
select * from multichain_router."**AnyswapV4Router_Mainstream_Coin2_evt_LogAnySwapOut"
```
### 山寨币桥:

(1) 合约地址：0xABd380327Fe66724FFDa91A87c772FB8D00bE488
```sql
select * from multichain_router."AnyswapV4Router_Altcoin_evt_LogAnySwapIn"
select * from multichain_router."AnyswapV4Router_Altcoin_evt_LogAnySwapOut"
```
## 一些研究中发现的细节
跨链桥中From和To都可以为自身，表示为跨链自身钱包账户中，尤其是EVM兼容的链，地址相同
但也可以通过跨链的方式发送给其他钱包地址，因此**在计算用户数时候，使用To作为因子计算更为准确。
参考案例：
1.跨链到自身钱包
[https://bscscan.com/tx/0x065c46071b9ec02570c30460e661c189745664b4b8de9f2f54a18501966a81bf#eventlog](https://bscscan.com/tx/0x065c46071b9ec02570c30460e661c189745664b4b8de9f2f54a18501966a81bf#eventlog)
2.跨链到另外一个钱包
[https://bscscan.com/tx/0xdba5484c3e323050bc7d8dbf20e415a4c326661214024e9900983e5409495e3a#eventlog](https://bscscan.com/tx/0xdba5484c3e323050bc7d8dbf20e415a4c326661214024e9900983e5409495e3a#eventlog)
