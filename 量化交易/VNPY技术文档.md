文档地址：[VeighNa用户文档 (vnpy.com)](https://www.vnpy.com/docs/cn/index.html)
## 环境准备
#### 软件安装
- vscode 或者 Pycharm
- [[mysql]]
	- 新建数据库vnpy，字符集utf8mb4，排序规则utf8mb4_general_ci
- vnpy 自带 python 环境
## 安装配置
- 下载安装包
https://download.vnpy.com/veighna_studio-3.8.0.exe
- 安装vnpy，指定安装目录
#### 快速上手
- 基本项目结构
```bash
/.vntrader
	/log
	connect_ctp.json
	cta_strategy_setting.json
	vt_setting.json
	...
/strategies
	DemoStrategy.py
	...
run.py
```
- 程序入口
```python
import sys

# 事件引擎
from vnpy.event import EventEngine

# 主引擎
from vnpy.trader.engine import MainEngine

# UI
from vnpy.trader.ui import MainWindow, create_qapp

# CTP 连接器
from vnpy_ctp import CtpGateway

# CTA自动交易模块
from vnpy_ctastrategy import CtaStrategyApp

# CTA回测研究模块
from vnpy_ctabacktester import CtaBacktesterApp

# 历史数据管理模块
from vnpy_datamanager import DataManagerApp

# 实盘行情记录模块
from vnpy_datarecorder import DataRecorderApp

# 风险管理模块
from vnpy_riskmanager import RiskManagerApp

def main():

    """"""

	# 创建应用
    q_app = create_qapp()
    event_engine = EventEngine()
    main_engine = MainEngine(event_engine)

    # 加载连接器
    main_engine.add_gateway(CtpGateway)
    # 加载功能模块
    main_engine.add_app(CtaStrategyApp)
    main_engine.add_app(CtaBacktesterApp)
    main_engine.add_app(ChartWizardApp)
    main_engine.add_app(DataManagerApp)
    main_engine.add_app(DataRecorderApp)
    main_engine.add_app(RiskManagerApp)

	# 主窗口
    main_window = MainWindow(main_engine, event_engine)
    main_window.showMaximized()
    q_app.exec()

if __name__ == "__main__":
    main()
```

## 数据
#### Tick 级别数据
Tick级别数据指的是以交易为单位记录的价格和成交量的时间序列数据。


## 交易接口


## CTA 策略
#### CTA 策略模版
[[template]]
```python
# ../vnpy/Lib/site-packages/vnpy_ctastrategy/template.py

class CtaTemplate(ABC):
	pass
```
参数配置：parameters = \[\]
变量配置：variables = \[\]

| 回调函数   | 函数名        |
| ---------- | ------------- |
| 策略初始化 | on_init       |
| 策略启动   | on_start      |
| 策略停止   | on_stop       |
| 行情推送   | on_tick       |
| 委托推送   | on_order      |
| 停止单推送 | on_stop_order |
| 成交推送   | on_trade      |
| K线推送    | on_bar        | 

| 交易函数     | 函数名       |
| ------------ | ------------ |
| 买入开仓     | buy          |
| 卖出平仓     | sell         |
| 卖出开仓     | short        |
| 买入平仓     | cover        |
| 撤销特定委托 | cancel_order |
| 撤销全部委托 | cancel_all   | 

| 功能函数 | 函数名          |
| -------- | --------------- |
| 输出日志 | write_log       |
| 发送邮件 | send_email      |
| 更新界面 | put_event       |
| 查询状态 | get_engine_type |
| 同步数据 | sync_data       | 

#### 策略开发

```dataview
list 
from ""
where contains(file.name,"策略")
```

## 历史回测
#### 回测

#### 代码编写

#### 参数优化

#### 回测结果评价


## 自动化交易

## 策略应用


## K线合成
调用或者重写[[K线合成器]]实现自定义K线合成

## 时间序列


## 扩展指标


## 条件逻辑

