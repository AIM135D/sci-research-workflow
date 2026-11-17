---
name: sci-novelty-check
description: SCI 创新筛选的单 Agent 查新阶段；比较候选机制与可核验最近邻论文，判断重合与证据缺口。
---
# SCI 单 Agent 查新

方法参考 [ARIS novelty-check](https://github.com/wanshuiyin/Auto-claude-code-research-in-sleep/blob/main/skills/novelty-check/SKILL.md)，仅借鉴主张拆解和多来源检索；不调用其指定模型、跨模型审稿、MCP reviewer 或自动派单。

拆解方法、目标、关键机制、训练策略和可检验贡献；为每个关键主张检索同义词、相邻领域、近期会议与预印本，记录搜索日期、范围与访问状态。优先比较实际论文方法而非标题；无全文或缺少关键信息时标注不足，至少两个可用独立来源核验关键文献身份。给出论文标题、作者、年份、原始链接、阅读层级、各项机制差异及证据锚点。不能上传未公开内容而未获授权。

输出 PROCEED（差异有可核验依据且无已知致命缺陷）、REVISE（有具体可修正重合或问题）、REJECT（明确已有工作重合或明确致命缺陷，提供证据）、INSUFFICIENT EVIDENCE（关键证据缺失）。邻近热门不等于否定，没有检索到也不等于首创。输出未解决争议、覆盖局限和下一步验证；不得声称独立跨模型审稿。
