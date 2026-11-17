# 安装与配置

本项目提供的是指令文件、角色配置和模板。实际执行取决于 Codex 客户端、模型与工具权限、网络连接以及研究者提供的材料。仓库不包含模型权重、数据库账号或自动实验环境。

## 在仓库中使用

安装 Git 和可用的 Codex 客户端后，克隆本仓库并在仓库根目录打开 Codex：

```bash
git clone https://github.com/AIM135D/sci-research-workflow.git
cd sci-research-workflow
```

Codex 的仓库级 Skill 位于 `.agents/skills/`。每个文件夹必须同时保留 `SKILL.md` 与该 Skill 需要的 `references/`。如技能列表没有更新，可重启客户端并检查当前工作目录。以当前的 [Codex Skill 官方说明](https://developers.openai.com/codex/skills) 为准。

macOS、Linux 和 Windows 的 Git 命令相同。Windows 用户可在 PowerShell 中运行上述命令；如果 GitHub 需要代理，请按自己的网络环境单独配置，不要把代理账号、密码或令牌写入仓库。

## 加入现有研究项目

1. 先检查目标项目的 `AGENTS.md`、`.agents/skills/` 和 `.codex/` 是否已有内容，备份需要修改的文件。
2. 按需复制整个 Skill 文件夹到目标项目的 `.agents/skills/`；保留 `references/` 及其他随附文件。
3. 若要使用角色，逐个比较并复制 `.codex/agents/` 中需要的角色文件。检查目标项目的 `.codex/config.toml`，将相关设置合并到现有配置，避免覆盖用户原有设置。
4. 阅读目标项目和用户的指令，确认写作语言、模型、网络、隐私与实验权限。仓库内示例不会自动赋予额外权限。

同名 Skill 可能同时出现在项目级和用户级目录；查看客户端列出的实际路径，避免把同名的不同版本误认为同一个文件。不同客户端或版本可能使用不同的发现方式，不能仅凭文件存在就断言已加载。

### Skill 之间的关系

| 使用场景 | 需要同时保留的仓库文件 |
| --- | --- |
| 论文写作或润色 | `sci-manuscript-writing/`，包括其 `references/` |
| 文献检索或只读审查 | 对应的 `sci-literature-search/` 或 `sci-peer-review/`，包括其 `references/` |
| 创新筛选 | `sci-innovation-selection/`；根据需要的阶段，同时保留 `sci-literature-search/`、`sci-novelty-check/`、`sci-research-refine/`、`sci-experiment-plan/`，后续写作可使用 `sci-manuscript-writing/` |

每个路径相对于 `.agents/skills/`。创新筛选按请求选择阶段，因此不需要每次都读取所有 Skill。项目没有内置学术数据库访问服务；某个工具不可用时需要报告并使用实际可用、经授权的来源。

## 验证一次安装

先让 Codex 列出或读取目标目录中的 `sci-manuscript-writing`。再提供一段**自己有权使用的**短文本，要求保留比较方向和限制条件；检查输出及实际读取的 Skill 路径。如果只需要诊断，明确要求只读。这个测试验证文件能否被使用以及一项具体行为，不能证明模型在所有任务中都可靠。

文献检索还需要可用的网络和合适的检索工具。某些服务可能需要账号或密钥；在目标环境自行配置，不要把凭据加入 Git。若原文不可访问，Skill 应标记阅读层级和证据缺口。

## 可选的多代理设置

项目包含 `.codex/config.toml` 和六份 `.codex/agents/*.toml`。角色文件只提供职责和行为说明，不写死模型。复制到其他项目之前，检查客户端版本、当前模型选择和并发限制；合并而不是直接替换现有配置。角色能否使用、是否支持显式模型选择及实际并发数量，以客户端和账户为准。官方配置细节见 [Codex Subagents](https://developers.openai.com/codex/multi-agent)。
