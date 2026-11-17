# SCI Research Workflow

A research workflow for Codex, covering literature discovery, novelty analysis, experimental planning, manuscript editing and author-side review. The researcher supplies the study evidence and makes final decisions. Use only the stages needed for the task.

## Included skills

| Task | Skill |
| --- | --- |
| Find and verify papers | [sci-literature-search](.agents/skills/sci-literature-search/SKILL.md) |
| Select research ideas | [sci-innovation-selection](.agents/skills/sci-innovation-selection/SKILL.md) |
| Compare novelty with prior work | [sci-novelty-check](.agents/skills/sci-novelty-check/SKILL.md) |
| Refine a research mechanism | [sci-research-refine](.agents/skills/sci-research-refine/SKILL.md) |
| Design a minimal experiment | [sci-experiment-plan](.agents/skills/sci-experiment-plan/SKILL.md) |
| Draft, translate or polish manuscripts | [sci-manuscript-writing](.agents/skills/sci-manuscript-writing/SKILL.md) |
| Review a manuscript without modifying it | [sci-peer-review](.agents/skills/sci-peer-review/SKILL.md) |

```bash
git clone https://github.com/AIM135D/sci-research-workflow.git
cd sci-research-workflow
```

Open Codex in the repository, or copy the needed skill directories into a target project's `.agents/skills/` after backing up any existing files. Skills are instructions; network access, models and data are provided by the user's environment. See the [installation guide](docs/installation.md) and the [official Codex skills documentation](https://developers.openai.com/codex/skills).

A solo agent is the default. Six optional, narrowly scoped role definitions are in `.codex/agents/`. Delegate only on explicit user request, with user-selected models and appropriate client support. An experiment plan does not authorize execution, and a reviewer does not edit the manuscript. Follow confidentiality and journal policies before processing third-party manuscripts.

By default, requested SCI manuscript drafting and editing starts with the requested Chinese text, then waits for the author's decision on English. Explicit English-only, translation, literal-only and read-only requests retain their stated scope. Preserve results, comparison direction, uncertainty, limitations and citations. The workflow does not guarantee publication or validate fabricated evidence.

Detailed guides and examples are currently in Chinese: [workflow](docs/workflow.md), [writing and review](docs/writing-review.md), [multi-agent use](docs/multi-agent.md), and [example prompts](examples/example-prompts.md). See [LICENSE](LICENSE) and [third-party notices](THIRD_PARTY_NOTICES.md).
