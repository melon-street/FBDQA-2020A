# Memo 4
## 金融基础知识
1. 金融基础概念
	* 资金融通、研究跨期配置稀缺资源的一门学科
		* 跨期：货币的时间价值
	* 公司金融
		* 财务会计
	* 资产定价
		* 金融工程
	* 基本假设：理性人假说
	* 边界条件：资源稀缺性与制度费用
	* 重要概念：选择、机会成本、偏好（风险厌恶、风险中性、风险偏好）、效用、信息（有效市场假说，捕捉市场的错误获得信息优势，通过技术指标获得更多信息）、预测
	* 基本原理：收益与风险权衡、边际效益递减
	* 理论支柱：有效市场假设、均值方差组合、CAPM、期权定价BS模型
2. 金融市场与制度
	* 直接融资市场、间接融资市场
	* 课程主要关注二级市场
	* 参与者：银行保险、券商、基金、信托
3. 金融资产
	* 金融资产本身没有使用价值
	* 流动性：大盘股大于小盘股，流动性递减风险递增
4. 交易制度
	* T+1,涨跌停
	* 卖空，只能融资融券
	* 新三板不属于A股，沪深300
5. 资产定价与投资学
	* 折现现金流模型
	* 研究return,债券：信用和久期
	* CAPM、三因子、四因子、五因子模型
	* 年化收益、夏普比率
6. CAPM 实证分析
## 聚宽平台
## 量化交易策略开发案例
1. 股票池
	* 市场、买入卖出、头寸
	* 没有期货的杠杆
2. 择时
3. 聚宽
	* 准备开盘前的数据 Initialize()/run_daily(..time = "before_open"...)
	* 拿到价格数据等，计算择时信号，盘中操作 run_daily(pl_trade,time = "every_bar")
	* 收盘之后，统计仓位情况，调整参数
	* 每天，只会在开盘调用一次，其他期间不会调用；分钟，pl_trade函数每分钟调用一次
	* 趋势型策略：赔率比胜率重要
	* 震荡型：胜率重要
	* 头寸管理最重要
4. 股票池
	* 构造优质股票集合，等待择时信号
	* 三要素
	 	* 选股条件：eg上证50成分股、市值
	 	* 再平衡： 多长时间重新调整一下成分股
	 	* 容量：多少支，多大规模资金
	* ROE净资产收益率，衡量公司质量，ROE不是越大越好
	* PE10~30，衡量估值，没有太被高估
5. 实例
	* 标定物、real price、滑点：保证成交以稍微高一点的价格买入
	* g. 全局变量
	* updated_stock 是否到交易时间，没有更新股票池什么都不做
	* order_value 下单
	* position 是持仓，不在新股票池，卖出去 order_target 仓位调整为0
6. 择时信号
	* 金叉买入：5日均线上穿30日均线，短时、长时均线 ；金叉判断往前回溯2个数据
	* 死叉卖出：5日均线下穿30日均线
	* 技术指标：MA.MACD.KDJ.RSI