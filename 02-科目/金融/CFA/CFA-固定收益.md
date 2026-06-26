---
aliases: [Fixed Income, 固定收益, 债券]
tags: [CFA, 固定收益, 金融]
created: 2026-06-26
source: 通用金融知识，待主人提供 CFA 教材后修正
---

# 固定收益（Fixed Income）

> ⚠️ **来源说明：** 以下内容基于通用债券市场知识整理，非特指某版 CFA 教材。待主人提供教材后补充具体例题。

## 债券基本特征

| 要素 | 说明 |
|------|------|
| 面值（Par/Face Value） | 通常为 1000 美元 |
| 票面利率（Coupon Rate） | 每年支付的利息占面值比例 |
| 到期日（Maturity） | 债券到期偿还面值的日期 |
| 发行人（Issuer） | 政府、公司、金融机构等 |

## 债券定价

### 基本定价公式

$$P = \sum_{t=1}^{n} \frac{C}{(1+r)^t} + \frac{FV}{(1+r)^n}$$

- C = 每期票息
- r = 要求收益率（YTM）
- n = 剩余期数
- FV = 面值

### 价格与收益率关系

- **YTM > 票面利率** → 折价（Discount）
- **YTM = 票面利率** → 平价（Par）
- **YTM < 票面利率** → 溢价（Premium）

## 利率风险度量

### 久期（Duration）

**麦考利久期（Macaulay Duration）：**

$$D_{Mac} = \frac{\sum_{t=1}^{n} t \times \frac{CF_t}{(1+y)^t}}{P}$$

**修正久期（Modified Duration）：**

$$D_{Mod} = \frac{D_{Mac}}{1 + y/m}$$

- 修正久期衡量利率变动 1% 时，债券价格变动的百分比
- **久期越长，利率风险越大**

### 凸度（Convexity）

$$\Delta P \approx -D_{Mod} \times \Delta y + \frac{1}{2} \times Convexity \times (\Delta y)^2$$

- 凸度是久期的补充，捕捉价格-收益率曲线的弯曲程度
- 正凸度对投资者有利（利率下降时涨得多，利率上升时跌得少）

## 信用分析

- **信用评级**：AAA → AA → A → BBB → BB → B → CCC → CC → D
- **投资级**：BBB- 及以上
- **高收益（垃圾债）**：BB+ 及以下
- 信用利差（Credit Spread）：风险债券与无风险债券的收益率差

---

*待主人提供教材后补充具体例题和版本信息 🧋*
