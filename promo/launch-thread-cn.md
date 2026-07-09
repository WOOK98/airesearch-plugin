# X 中文 Launch Thread — airesearch-plugin

---

**Tweet 1 (Hook)**

在 Claude Code 里输入 `/deep-dive NVDA`，拿到一份六维度个股深度报告——供应链、基本面、宏观、技术面、情绪、风险矩阵，不是 LLM 猜的。

装一个插件就行。

---

**Tweet 2 (供应链)**

供应链维度会拆解：NVDA 的前五大供应商是谁、下游客户集中度多少、哪条产品线贡献了最多收入。

数据来源是 MCP server 的 `resolve_entity` + `get_financials`，不靠搜索拼凑。（实时数据需接 MCP 数据层，无 key 时走 web search。）

Prompt: `/deep-dive NVDA supply-chain`

---

**Tweet 3 (基本面)**

基本面维度直接拉 Yahoo Finance 的 GAAP 数据：TTM 收入、毛利率、FCF、EV/EBITDA。

不会出现"根据我的训练数据"这种话——每个数字都有来源标注。

Prompt: `/deep-dive AMD fundamentals`

---

**Tweet 4 (技术面)**

技术面是确定性计算，不是 LLM 估计：RSI、MACD、20/50/200 日均线、ATR，全部从日线 OHLCV 算出来的。

Prompt: `/deep-dive TSLA technicals`

---

**Tweet 5 (行业模式)**

输入一个主题而不是 ticker，比如"humanoid robot"，它会自动解析相关 ETF，拉持仓数据，构建产业链 universe。

Prompt: `/deep-dive "humanoid robot"`

这是最实用的功能——不用自己翻 ETF 持仓表了。

---

**Tweet 6 (快照)**

不需要完整报告时用 `/snapshot`：一个结构化快照，适合盘中快速决策。

Prompt: `/snapshot MU`

---

**Tweet 7 (安装)**

安装：

```
/plugin marketplace add WOOK98/airesearch-plugin
/plugin install airesearch@airesearch-marketplace
```

不需要 API key 就能用——没有 key 时自动走 web search。
想要实时市场数据？DM @wook98 或 email hello@airesearchs.com 拿 beta key。

→ [github.com/WOOK98/airesearch-plugin](https://github.com/WOOK98/airesearch-plugin)

---

**Tweet 8 (底线)**

这个插件不给投资建议。它提供结构化数据和分析框架，投资决策是你自己的事。

六个维度的分析方法论来自 @aleabitoreddit 的公开框架，数据来自 Yahoo Finance 和实时行情 API。
