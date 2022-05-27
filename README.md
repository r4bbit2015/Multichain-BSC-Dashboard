# Multichain-BSC-Dashboard
Probably nothing.  
数据的解析至关重要，只要能解析获取到数据，就可以画出任何想要的图表
# 路由桥概述

路由分为2个主流币，2个原生币，1个山寨币

|   No  |  Name |  Address   |
|  ----  | ----  | ----  |
| 1 |原生币    | 0x92c079d3155c2722dbf7e65017a5baf9cd15561c |
| 2 |原生币    | 0xf9736ec3926703e85c843fc972bd89a7f8e827c0 |
| 3 |主流币     | 0xd1C5966f9F5Ee6881Ff6b261BBeDa45972B1B5f3 |
| 4 |主流币      | 0xe1d592c3322f1f714ca11f05b6bc0efef1907859 |
| 5 |山寨币        | 0xABd380327Fe66724FFDa91A87c772FB8D00bE488 |





### 原生币桥
(1) 合约地址：0x92c079d3155c2722dbf7e65017a5baf9cd15561c
```sql
select * from multichain_router."AnyswapV6Router_Native_Coin1_evt_LogAnySwapIn"
select * from multichain_router."AnyswapV6Router_Native_Coin1_evt_LogAnySwapOut"
```
(2) 合约地址：0xf9736ec3926703e85c843fc972bd89a7f8e827c0
```sql
select * from  multichain_router."AnyswapV3Router_Native_Coin2_evt_LogAnySwapIn"
select * from  multichain_router."AnyswapV3Router_Native_Coin2_evt_LogAnySwapOut"
```

### 主流币桥
(1) 合约地址：0xd1C5966f9F5Ee6881Ff6b261BBeDa45972B1B5f3
```sql
select * from multichain_router."AnyswapV4Router_Mainstream_Coin1_evt_LogAnySwapIn"
select * from multichain_router."AnyswapV4Router_Mainstream_Coin1_evt_LogAnySwapOut"
```
(2) 合约地址：0xe1d592c3322f1f714ca11f05b6bc0efef1907859
```sql
select * from multichain_router."AnyswapV4Router_Mainstream_Coin2_evt_LogAnySwapIn"
select * from multichain_router."AnyswapV4Router_Mainstream_Coin2_evt_LogAnySwapOut"
```
### 山寨币桥
(1) 合约地址：0xABd380327Fe66724FFDa91A87c772FB8D00bE488
```sql
select * from multichain_router."AnyswapV4Router_Altcoin_evt_LogAnySwapIn"
select * from multichain_router."AnyswapV4Router_Altcoin_evt_LogAnySwapOut"
```

### 接口提交没有通过更换为使用ethereum."log"   

|函数名  | Topics  |
|  ----  | ---- |
|LogAnySwapIn | 0xaac9ce45fe3adf5143598c4f18a369591a20a3384aedaf1b525d29127e1fcd55 |
|LogAnySwapOut| 0x97116cf6cd4f6412bb47914d6db18da9e16ab2142f543b86e207c24fbd16b23a |

  
  
### LogAnySwap(In/Out)数据解析
Example:
```python
a = x00000000000000000000000000000000000000000000000002e57ca3a3126000000000000000000000000000000000000000000000000000000000004e4541520000000000000000000000000000000000000000000000000000000000000038
```
```python
substring(DATA::text, 0,67) AS "amount",
0x00000000000000000000000000000000000000000000000002e57ca3a3126000
substring(DATA::text, 68,63) AS "fromChainID", #没错，就是68-63，不知道为啥
000000000000000000000000000000000000000000000000000000004e454152
substring(DATA::text, 132,193) AS "toChainID",
0000000000000000000000000000000000000000000000000000000000000038
```
### From/To解析
IN和OUT中Topic并不相同  
### In:    
* topic1 - 判断调用函数名(in/out)
* topic2 - 不知道是啥 - address indexed account 
* topic3 - Token合约地址
* topic4 - To地址


### Out  
* topic1 - 判断调用函数名(in/out)
* topic2 - Token合约地址
* topic3 - From地址
* topic4 - To地址  


# 桥概述
2个ETH、9个BSC、1个btc、1个fsn

|   Type  |  Name |  Address   |  Type  |
|  ----  | ----  | ----  |----  |
| 1 |eth-2-bsc-v1     | 0x13B432914A996b0A48695dF9B2d701edA45FF264 |A |
| 2 |eth-2-bsc-v2     | 0x533e3c0e6b48010873b947bddc4721b1bdff9648 |A |
| 3 |bsc-2-avax       | 0xb1CB88B1a1992deB4189Ea4f566b594c13392Ada |B |
| 4 |bsc-2-matic      | 0x171a9377C5013bb06Bca8CfE22B9C007f2C319F1 |B |
| 5 |bsc-2-ftm        | 0x4b3B4120d4D7975455d8C2894228789c91a247F8 |B |
| 6 |bsc-2-moonriver  | 0xd6faf697504075a358524996b132b532cc5D0F14 |B |
| 7 |bsc-2-arbitrum   | 0xAd1A0d92db9157ac9EF7ee74Be38940f60BcafA9 |B |
| 8 |btc-2-bsc        | 0x930a7F05C5e38eaF90493325F8106806969FCBdF |A |
| 9 |fsn-2-bsc        | 0xf38C36bc1B2Fe5E9029C91AB520457bE7DFC68D8 |A |
| 10 |bsc-2-eth        | 0xB16E3336699A636DD6C8246A3a12b813bFa0A3AD |B |
| 11 |bsc-2-kcc        | 0x88036021b39759Fc46aD79850679282cb2353372 |B |
| 12 |bsc-2-okc        | 0x63a3d28bB9187809553dD16981C73f498B6b2687 |B |
| 13 |bsc-2-moombeam   | 0xd9B4aE62721d6311d67566A32E75f9002447922e |B |

## 桥数据解析
## A类型桥
IN-BSC(in在bsc链上可以找到）
只有out，没有in，所有的in都是假币
out其实就是in
token从桥转出,到用户钱包地址，这是用户将Token跨链到BSC的行为，所以为in
用户跨链到ETH的行为并不在BSC链上，而是在ETH链上

OUT-ETH（out的数据在ETH链上）
由于这个桥使用的是Transfer事件/函数，所以无法直接使用topic过滤交易，需要增加条件语句，限定form方地址
topic2 = from方地址 (桥地址)

|函数名  | Topics  |
|  ----  | ---- |
|LogSwapin | 0x05d0634fe981be85c22e2942a880821b70095d84e152c3ea3c17a4e4250d9d61 |
|Transfer| 此处使用log获取数据太慢，应该使用transactions|

Demo:  
```sql
select
"to" as "To_address"
from
  ethereum."transactions"
WHERE
  "from" = '\x13b432914a996b0a48695df9b2d701eda45ff264'
```
### In:    
* topic1 - 判断调用函数名(in/out)
* topic2 - 不知道是啥 - address indexed account 
* topic3 - To地址
### Out:
out数据在eth链上，无法同时获取

## A类型数据解析Demo:
```sql
with bridgedata as (
SELECT contract_address,tx_hash,bytea2numeric(data) as "amount" from bsc."logs"
WHERE topic1='\x05d0634fe981be85c22e2942a880821b70095d84e152c3ea3c17a4e4250d9d61'
 
)
select * from bridgedata
```



## B类型桥
这些桥的跨链逻辑为：  
用户A发送Token到BSC链上->IN(资产跨入BSC)  
跨链桥流程：   
1.将用户A所在链的Token销毁到0x000地址  
2.从BSC链上发送Token给用户A  
在BSC链上只能看到桥地址将Token转出到用户A地址上（OUT即IN）  
相反的操作  
用户A从BSC跨链到AVAX链->OUT(资产跨出BSC)  
1.用户A资产转入BSC桥中（冻结资产，保证和avax链上1:1)  
2.AVAX链将资产发送给用户A（此处资产为anyswap mint 的token）  

### B类型桥数据解析
```sql
--  avax 
select "to","block_hash" 
from bsc."transactions" 
where "from" = '\xb1cb88b1a1992deb4189ea4f566b594c13392ada'

select "from" ,hash
from bsc."transactions" 
where "to" = '\xb1CB88B1a1992deB4189Ea4f566b594c13392Ada'

-- matic 
select "to","block_hash" 
from bsc."transactions" 
where "from" = '\xb1cb88b1a1992deb4189ea4f566b594c13392ada'

select "from" ,hash
from bsc."transactions" 
where "to" = '\xb1CB88B1a1992deB4189Ea4f566b594c13392Ada'

-- fantom
select "to","block_hash" 
from bsc."transactions" 
where "from" = '\x4b3B4120d4D7975455d8C2894228789c91a247F8'

select "from" ,hash
from bsc."transactions" 
where "to" = '\x4b3B4120d4D7975455d8C2894228789c91a247F8'

-- moonriver
select "to","block_hash" 
from bsc."transactions" 
where "from" = '\xd6faf697504075a358524996b132b532cc5D0F14'

select "from" ,hash
from bsc."transactions" 
where "to" = '\xd6faf697504075a358524996b132b532cc5D0F14'

-- Arbitrum

select "to","block_hash" 
from bsc."transactions" 
where "from" = '\xAd1A0d92db9157ac9EF7ee74Be38940f60BcafA9'

select "from" ,hash
from bsc."transactions" 
where "to" = '\xAd1A0d92db9157ac9EF7ee74Be38940f60BcafA9'

-- bsc-2-eth 
select "to","block_hash" 
from bsc."transactions" 
where "from" = '\xB16E3336699A636DD6C8246A3a12b813bFa0A3AD'

select "from" ,hash
from bsc."transactions" 
where "to" = '\xB16E3336699A636DD6C8246A3a12b813bFa0A3AD'

-- bsc-2-okc	
select "to","block_hash" 
from bsc."transactions" 
where "from" = '\x63a3d28bB9187809553dD16981C73f498B6b2687'

select "from" ,hash
from bsc."transactions" 
where "to" = '\x63a3d28bB9187809553dD16981C73f498B6b2687'

-- bsc-2-moombeam	
select "to","block_hash" 
from bsc."transactions" 
where "from" = '\xd9B4aE62721d6311d67566A32E75f9002447922e'

select "from" ,hash
from bsc."transactions" 
where "to" = '\xd9B4aE62721d6311d67566A32E75f9002447922e'
```

# API
API可用来检查Dune上的数据是否准确，以及参照API中的路由/桥信息可快速掌握链ID对应的链名称
##支持的链/链ID
https://bridgeapi.anyswap.exchange/data/allBridgeChainInfo

PostgreSQL合约地址-代币符号-用于识别代币Symbol  
https://github.com/r4bbit2015/Multichain-BSC-Dashboard/blob/main/Token-address-symbol.sql

PostgreSQL合约精度-用于计算TVL  
https://github.com/r4bbit2015/Multichain-BSC-Dashboard/blob/main/Token-address-decimal.sql


# 手续费计算 
对于非 ETH 链：每笔交易 0.9 美元；    
至 ETH：每笔交易 0.1%；最低费用 50 美元；最高收费1000美元。  

参考资料：https://medium.com/multichainorg/anyswap-fees-explained-bceddf535b83

## 一些研究中发现的细节
跨链桥中From和To都可以为自身，表示为跨链自身钱包账户中，尤其是EVM兼容的链，地址相同 
但也可以通过跨链的方式发送给其他钱包地址，因此在计算用户数时候，使用To作为因子计算更为准确。    
参考案例：    
1.跨链到自身钱包     
https://bscscan.com/tx/0x065c46071b9ec02570c30460e661c189745664b4b8de9f2f54a18501966a81bf#eventlog  
2.跨链到另外一个钱包     
https://bscscan.com/tx/0xdba5484c3e323050bc7d8dbf20e415a4c326661214024e9900983e5409495e3a#eventlog  


# 无法解决的问题
eth-2-bsc-v1/eth-2-bsc-v2 这两个桥中的in和out在eth/bsc链上，dune无法同时使用bsc和eth
