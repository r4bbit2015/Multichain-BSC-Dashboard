SELECT 
    COUNT(DISTINCT(
        CASE WHEN `to` = '0x6238872a0bd9f0e19073695532a7ed77ce93c69e' THEN `from` ELSE `to` END
    )) AS total_user
FROM `bnb`.`transactions`
WHERE block_time >= '2022-04-01 00:00'
AND (`from` = '0x6238872a0bd9f0e19073695532a7ed77ce93c69e' OR `to` = '0x6238872a0bd9f0e19073695532a7ed77ce93c69e') -- StepN Wallet
AND `from` != '0x0000000000000000000000000000000000000000'
AND `from` != '0x0000000000000000000000000000000000000000' -- remove mint
AND `to`!= '0x000000000000000000000000000000000000dEaD' -- remove burn
AND `to` != '0x0000000000000000000000000000000000000000' -- remove burn
AND `from` != '0xfcfc7130e8af8c016823fa06d00d7c512c61ac7f'  -- remove offical add liquid wallet
AND `to` != '0xfcfc7130e8af8c016823fa06d00d7c512c61ac7f'  -- remove offical add liquid wallet
AND success

