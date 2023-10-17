## 基本API

## 下载全市场期货数据和更新

```python
# 设置合约品种
symbols = {
    "SHFE": ["CU", "AL", "ZN", "PB", "NI", "SN", "AU", "AG", "RB", "WR", "HC", "SS", "BU", "RU", "NR", "SP", "SC", "LU", "FU"],
    "DCE": ["C", "CS", "A", "B", "M", "Y", "P", "FB","BB", "JD", "RR", "L", "V", "PP", "J", "JM", "I", "EG", "EB", "PG"],
    "CZCE": ["SR", "CF", "CY", "PM","WH", "RI", "LR", "AP","JR","OI", "RS", "RM", "TA", "MA", "FG", "SF", "ZC", "SM", "UR", "SA", "CL"],
    "CFFEX": ["IH","IC","IF", "TF","T", "TS"]
}
symbol_type = "99"

# 设置下载时间
from datetime import datetime
start_date = datetime(2005,1,1)
end_date = datetime(2020,9,10)

# 批量下载
# 调用数据下载模块和数据保存模块


# 定时批量下载
from datetime import datetime, time
from time import sleep
​
current_time = datetime.now().time()
start_time = time(17,0)
​
while True:
  sleep(10)
  
  if current_time == start_time:
    download_data()

# 获取数据库数据

```

## vnpy 数据库
### dbbardata
```sql
CREATE TABLE `dbbardata` (
  `CREATE TABLE `dbbardata` (
  `id` int NOT NULL AUTO_INCREMENT, -- 主键
  `symbol` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 交易标的代码
  `exchange` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 交易所
  `datetime` datetime NOT NULL, -- 时间
  `interval` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 时间间隔
  `volume` float NOT NULL, -- 成交量
  `turnover` float NOT NULL, -- 成交额
  `open_interest` float NOT NULL, -- 持仓量
  `open_price` float NOT NULL, -- 开盘价
  `high_price` float NOT NULL, -- 最高价
  `low_price` float NOT NULL, -- 最低价
  `close_price` float NOT NULL, -- 收盘价
  PRIMARY KEY (`id`), -- 主键约束
  UNIQUE KEY `dbbardata_symbol_exchange_interval_datetime` (`symbol`, `exchange`, `interval`, `datetime`) -- 唯一约束
) ENGINE=InnoDB AUTO_INCREMENT=234391 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;
```
### dbbaroverview
```sql
CREATE TABLE `dbbaroverview` (
  `id` int NOT NULL AUTO_INCREMENT, -- 主键
  `symbol` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 交易标的代码
  `exchange` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 交易所
  `interval` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 时间间隔
  `count` int NOT NULL, -- 数据数量
  `start` datetime NOT NULL, -- 起始时间
  `end` datetime NOT NULL, -- 结束时间
  PRIMARY KEY (`id`), -- 主键约束
  UNIQUE KEY `dbbaroverview_symbol_exchange_interval` (`symbol`, `exchange`, `interval`) -- 唯一约束
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;
```
### dbtickdata
```sql
CREATE TABLE `dbtickdata` (
  `id` int NOT NULL AUTO_INCREMENT, -- 主键
  `symbol` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 交易标的代码
  `exchange` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 交易所
  `datetime` datetime(3) NOT NULL, -- 时间戳（带毫秒）
  `name` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 名称
  `volume` float NOT NULL, -- 成交量
  `turnover` float NOT NULL, -- 成交额
  `open_interest` float NOT NULL, -- 持仓量
  `last_price` float NOT NULL, -- 最新价格
  `last_volume` float NOT NULL, -- 最新成交量
  `limit_up` float NOT NULL, -- 涨停价
  `limit_down` float NOT NULL, -- 跌停价
  `open_price` float NOT NULL, -- 开盘价
  `high_price` float NOT NULL, -- 最高价
  `low_price` float NOT NULL, -- 最低价
  `pre_close` float NOT NULL, -- 昨收盘价
  `bid_price_1` float NOT NULL, -- 买一价
  `bid_price_2` float DEFAULT NULL, -- 买二价
  `bid_price_3` float DEFAULT NULL, -- 买三价
  `bid_price_4` float DEFAULT NULL, -- 买四价
  `bid_price_5` float DEFAULT NULL, -- 买五价
  `ask_price_1` float NOT NULL, -- 卖一价
  `ask_price_2` float DEFAULT NULL, -- 卖二价
  `ask_price_3` float DEFAULT NULL, -- 卖三价
  `ask_price_4` float DEFAULT NULL, -- 卖四价
  `ask_price_5` float DEFAULT NULL, -- 卖五价
  `bid_volume_1` float NOT NULL, -- 买一量
  `bid_volume_2` float DEFAULT NULL, -- 买二量
  `bid_volume_3` float DEFAULT NULL, -- 买三量
  `bid_volume_4` float DEFAULT NULL, -- 买四量
  `bid_volume_5` float DEFAULT NULL, -- 买五量
  `ask_volume_1` float NOT NULL, -- 卖一量
  `ask_volume_2` float DEFAULT NULL, -- 卖二量
  `ask_volume_3` float DEFAULT NULL, -- 卖三量
  `ask_volume_4` float DEFAULT NULL, -- 卖四量
  `ask_volume_5` float DEFAULT NULL, -- 卖五量
  `localtime` datetime DEFAULT NULL, -- 本地时间
  PRIMARY KEY (`id`), -- 主键约束
  UNIQUE KEY `dbtickdata_symbol_exchange_datetime` (`symbol`, `exchange`, `datetime`) -- 唯一约束
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

```
### dbtickoverview
```sql
CREATE TABLE `dbtickoverview` (
  `id` int NOT NULL AUTO_INCREMENT, -- 主键
  `symbol` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 交易标的代码
  `exchange` varchar(255) COLLATE utf8mb4_general_ci NOT NULL, -- 交易所
  `count` int NOT NULL, -- 数据数量
  `start` datetime NOT NULL, -- 起始时间
  `end` datetime NOT NULL, -- 结束时间
  PRIMARY KEY (`id`), -- 主键约束
  UNIQUE KEY `dbtickoverview_symbol_exchange` (`symbol`, `exchange`) -- 唯一约束
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;
```


