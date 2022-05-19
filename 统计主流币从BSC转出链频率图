SELECT 
    CASE "toChainID"
      WHEN '1' THEN 'Ethereum'
      WHEN '10' THEN 'Optimism'
      WHEN '25' THEN 'Cronos'
      WHEN '66' THEN 'OKXChain'
      WHEN '137' THEN 'Polygon'
      WHEN '199' THEN 'BitTorrent'
      WHEN '250' THEN 'Fantom'
      WHEN '288' THEN 'BobaNetwork'
      WHEN '321' THEN 'KCCMainnet'
      WHEN '1284' THEN 'Moonbeam'
      WHEN '1285' THEN 'Moonriver'
      WHEN '42161' THEN 'Arbitrum'
      WHEN '43114' THEN 'Avalanche'
    END AS oven,
    COUNT(distinct "from") AS Counts
from multichain_v3."AnyswapV4RouterStableCoin_evt_LogAnySwapOut" 
Where "toChainID" IN(
    '1' ,
    '10', 
     '25' ,
     '56' ,
    '66' ,
    '137' ,
    '199' ,
    '250' ,
    '288' ,
    '321' ,
    '1284' ,
    '1285' ,
    '42161',
    '43114'
)
GROUP BY 1
