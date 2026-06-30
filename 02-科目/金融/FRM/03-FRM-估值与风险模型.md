---
aliases: [Value at Risk, VaR, 在险价值]
tags: [FRM, 估值与风险模型, 金融]
created: 2026-06-26
source: 通用风险管理知识，待主人提供 FRM 教材后修正
---

# 在险价值（Value at Risk, VaR）

> ⚠️ **来源说明：** 以下内容基于通用风险管理理论整理，非特指某版 FRM 教材。待主人提供教材后补充具体例题和版本信息。

## 定义

**VaR** 是在给定置信水平和时间期限下，投资组合可能遭受的**最大损失**。

> "We are X% confident that the loss will not exceed $Y over the next N days."

## 三种计算方法

### 1. 参数法（Parametric / Variance-Covariance）

$$VaR = \mu - z_\alpha \times \sigma$$

- 假设收益率服从**正态分布**
- zα = 对应置信水平的 z 值（95% → 1.645，99% → 2.326）
- **优点**：计算简单
- **缺点**：假设正态分布，不适用于厚尾分布

### 2. 历史模拟法（Historical Simulation）

- 直接用历史收益率分布
- 将历史收益率排序，取对应分位数
- **优点**：不需要分布假设
- **缺点**：依赖历史数据，无法预测未来极端事件

### 3. 蒙特卡洛模拟法（Monte Carlo Simulation）

- 随机模拟大量收益率路径
- 取对应分位数作为 VaR
- **优点**：灵活，可处理复杂产品
- **缺点**：计算量大，模型风险

## VaR 的局限性

- **不是最坏情况**：只告诉你在置信水平下的损失上限
- **不满足次可加性**：组合 VaR 可能大于各资产 VaR 之和
- **对尾部风险不敏感**：无法衡量极端损失

## 期望亏损（Expected Shortfall, ES / CVaR）

$$ES = E[Loss | Loss > VaR]$$

- 当损失超过 VaR 时的**平均损失**
- 满足次可加性，是**一致性风险度量**
- 巴塞尔协议 III 推荐使用 ES 替代 VaR

## 回测检验（Backtesting）

- 比较 VaR 预测与实际损失
- **Kupiec 检验**：检验突破频率是否符合预期
- 95% VaR，250 个交易日，预期突破 12.5 次

---

*待主人提供教材后补充具体例题和版本信息 🧋*
