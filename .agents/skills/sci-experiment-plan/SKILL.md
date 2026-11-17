---
name: sci-experiment-plan
description: 为 SCI 候选机制规划最低成本的可证伪实验；只设计不自动执行。
---
# SCI 最小实验计划

方法参考 [ARIS experiment-plan](https://github.com/wanshuiyin/Auto-claude-code-research-in-sleep/blob/main/skills/experiment-plan/SKILL.md) 的主张到证据与阶段化运行顺序；仅输出与用户范围相符的计划，不调用外部模型、训练或创建固定日志目录。

列出问题、假设和竞争解释，为每项关键主张确定最小区分性测试。明确数据来源、许可、划分、最强可行基线、公平算力比较、评价指标、关键变量、控制与消融、可重复性和不确定性；避免数据泄漏。按环境与数据检查、基线、最小方法、关键消融/停止决策排列，写出每一步成功、失败、不确定和停机条件。硬件以用户提供的信息为准；显存和时长为估算，未知标 UNKNOWN。区分必需实验和可选扩展。只有用户明确要求执行实验时才能实施，并遵循项目的存储及日志规则。
