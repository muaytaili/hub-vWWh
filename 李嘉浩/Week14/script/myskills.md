---
name: 股票可视化和买入卖出分析
description: 定义一个skill，包含对股票的可视化功能，对于股票的周波动、日波动绘制在一个图中，并基于大小给出一个买入卖出的最佳时间建议；

---

## 分析逻辑
1. 用户输入股票代码获取得到股票日k线（最近半年），进行画图 和 波动分析。
2. 我提供一个返回行情的api是https://api.autostock.cn/v1/stock/kline/day?code=000001，经过检查可以返回的数据结构是
{
  "code": 200,
  "message": "操作成功",
  "traceId": "...",
  "data": [
    ["日期", "开盘", "收盘", "最高", "最低", "成交量", ...], // 每一根K线数据
    ...
  ]
}
3.保存html通过bokeh 包来实现 

## 使用逻辑

```commandline
python script/plot_stock_and_analysis2.py --code=sh600519 --start=2026-01-01 --end=2026-05-10 --plot_save_path=./plot_stock_kline.html

python script/plot_stock_and_analysis2.py --code=sh600519 --start=2026-01-01 --end=2026-05-01 --plot_save_path=./stock_analysis.html

分析图表已成功保存为交互式网页: ./plot_stock_kline.html,另外一个网页为stock_analysis.html

--- 【最佳买卖时间建议】 ---
💡 建议【买入】日期: ['2026-03-27', '2026-03-30', '2026-04-23']
🚨 建议【卖出】日期: ['2026-03-23', '2026-03-24', '2026-04-30']
----------------------------
```

## 依赖环境
```commandline
bokeh
pandas
```
