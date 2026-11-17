# SCI Research Workflow

面向科研人员的 Codex 工作流，覆盖文献检索、创新性分析、实验设计、论文写作和作者侧审查。你可以只使用其中一个环节，也可以在已有证据的基础上串联多个环节。论文中的实验数据和结论由作者提供，助手负责组织、核对和指出缺口。

项目默认由一个主 Agent 完成任务。只有用户明确要求多代理时，才按当前客户端支持的方式启用专项角色。实验计划不会自动转化为训练任务，审查意见也不会自动修改论文。

## 可以用它做什么

| 你的任务 | 使用的 Skill | 预期交付 |
| --- | --- | --- |
| 找论文或核实研究依据 | [`sci-literature-search`](.agents/skills/sci-literature-search/SKILL.md) | 有链接、版本、阅读层级和证据状态的文献记录 |
| 筛选研究问题或比较机制 | [`sci-innovation-selection`](.agents/skills/sci-innovation-selection/SKILL.md) | 研究问题、最近邻差异、候选假设与待验证项 |
| 针对一个候选方案查新 | [`sci-novelty-check`](.agents/skills/sci-novelty-check/SKILL.md) | 与可核验近邻逐项比较，说明检索局限 |
| 细化已有机制 | [`sci-research-refine`](.agents/skills/sci-research-refine/SKILL.md) | 输入输出、关键机制、对照、预期收益和失败条件 |
| 设计最小验证 | [`sci-experiment-plan`](.agents/skills/sci-experiment-plan/SKILL.md) | 数据、基线、指标、预算、停止条件和可复现记录 |
| 起草、翻译或润色论文 | [`sci-manuscript-writing`](.agents/skills/sci-manuscript-writing/SKILL.md) | 所请求范围的稿件及需要作者核实的事项 |
| 只读审查论文 | [`sci-peer-review`](.agents/skills/sci-peer-review/SKILL.md) | 带位置、证据、影响和建议的分级问题清单 |

每个 Skill 都有自己的 `SKILL.md`。Codex 可以按任务匹配使用，也可以在提示中明确写出 Skill 名称。复杂工作应分阶段交付并由研究者决策，短段落润色不需要运行完整科研流程。

论文写作 Skill 参照原有中文表达与英文论文编辑工作流，整理成可随仓库使用的版本。它把语言编辑和科学一致性检查放在同一位写作负责人手中，并将作者侧审查单独列为只读任务。

## 快速开始

需要已安装且可使用的 Codex 客户端，以及本地 Git。克隆仓库后，在仓库目录中打开 Codex，或将所需 Skill 文件夹复制到目标项目的 `.agents/skills/` 中。已有同名文件时先比较并备份，再决定如何合并。

```bash
git clone https://github.com/AIM135D/sci-research-workflow.git
cd sci-research-workflow
```

进入仓库后，可以从一个有明确范围的请求开始：

```text
使用 sci-literature-search，围绕我给出的研究问题查找近期和基础文献。
请记录查询范围、来源、阅读层级和未能核验的信息，不要编造引用。
```

论文润色示例：

```text
使用 sci-manuscript-writing，只润色我提供的这一段中文。
保留数据、引用、比较方向、限制和不确定性；指出有歧义的地方。
```

如果只需要英文润色或中译英，请直接说明目标语言和范围。明确要求逐字翻译时，按直译处理；未公开第三方稿件应先确认有权使用当前工具。

Codex 的具体发现路径、客户端支持和权限可能随版本不同；参见 [安装与配置](docs/installation.md) 和 [OpenAI 官方 Skill 文档](https://developers.openai.com/codex/skills)。

## 工作流怎么衔接

```mermaid
flowchart LR
    Q[研究问题与约束] --> L[文献与证据]
    L --> N[查新与机制假设]
    N --> P[最小实验计划]
    P -->|用户授权执行| E[执行并记录结果]
    E --> I[解释与决策]
    I --> W[论文写作与润色]
    W --> R[只读审查]
    R -->|作者授权修改| W
```

箭头表示信息依赖，不表示每个任务都必须从头运行。证据不足时，先记录未解决的问题；未经授权，不将未公开想法、稿件或数据发送给外部服务。完整流程和各阶段的输入、输出及停止条件见 [工作流与决策指南](docs/workflow.md)。

## 六个可选角色

角色文件位于 [`.codex/agents/`](.codex/agents/)。主 Agent 负责界定任务、分派授权范围和最终判断。

| 角色 | 负责 | 不负责 |
| --- | --- | --- |
| `literature_scout` | 检索和核验论文与证据 | 对创新性作最终裁决或运行实验 |
| `novelty_architect` | 根据已有证据提出可证伪机制 | 独立启动大规模检索或训练 |
| `adversarial_reviewer` | 检查重合、泄漏、混杂和其他解释 | 修改稿件或给出期刊决定 |
| `experiment_designer` | 设计有预算和停止条件的验证 | 执行实验 |
| `experiment_engineer` | 在授权范围内实现并运行 | 擅自更改问题或启动未授权任务 |
| `paper_auditor` | 只读检查稿件与证据的一致性 | 改写稿件或宣称期刊审稿结论 |

用户明确启动多代理后，再确认角色、模型及可用客户端能力；需要什么角色就使用什么角色。角色指令是行为约束，并不构成独立的操作系统隔离。详见 [多代理使用指南](docs/multi-agent.md)。

## 写作与审查边界

论文中文起草和润色默认先交付用户请求的中文范围，是否进入英文阶段由用户决定。明确要求英文写作、中译英或英文润色时，直接处理所请求的英文任务。润色会检查数据、引用、比较对象、条件、负面结果和真实不确定性，不能用更流畅的表达掩盖证据缺口。

模拟审查是作者侧辅助工作。审查第三方投稿时，需要遵循相关授权、保密和期刊 AI 政策。工作流不能保证论文被接收、查新穷尽、检测器分数或实验结果；最终结论由研究者核实。详细说明见 [写作、翻译与审查](docs/writing-review.md)。

## 模板与示例

- [最小实验计划模板](templates/experiment-plan.md)：区分已知、假设、授权和未执行事项。
- [主张与证据模板](templates/claim-evidence.md)：将稿件结论对应到具体结果或文献位置。
- [示例任务](examples/example-prompts.md)：包含文献检索、创新查新、段落润色和论文审查的提示词。

模板使用占位符，没有内置论文、数据集或实验结果。检索能力、联网和模型可用性由使用者的环境决定；调用外部服务前应核查其数据处理和访问条件。

## 许可与来源

本仓库以 [MIT License](LICENSE) 发布。查新、方案细化与实验规划参考的第三方项目及其许可见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。本仓库未打包外部数据库服务、模型或部分可选 Skill，它们适用各自的条款。

English overview: [README.en.md](README.en.md).
