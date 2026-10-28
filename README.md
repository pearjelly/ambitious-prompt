# Ambitious Prompt

一个面向 Codex 的提示词优化 Skill。它根据任务，从高度、广度、深度、速度四个维度选择适用方法，明确目标、约束、证据和验收标准，再完成用户授权的任务。

Ambitious Prompt is a Codex skill that adapts prompt improvement methods to each task. It can improve a request before execution or return a reusable prompt without executing it. Previously named Task Compass and Prompt Upgrader.

## 方法来源

本项目的核心框架受到 Felix Rieseberg 的文章 [《How to be more ambitious: A tutorial for humans with models》](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/) 启发。Felix 是 Anthropic 的工程经理，曾负责 Claude.ai、Cowork 和 Claude Code Desktop 的工程工作。他在文中提出用四个维度思考如何更有野心地使用 AI：

- **高度（Altitude）**：关注任务背后想达到的结果。
- **广度（Range）**：引入不同领域的知识、工具和方法。
- **深度（Depth）**：运用专业方法、原始数据和外部检验，把问题做深。
- **速度（Speed）**：用更少时间完成工作。

原文重点展开高度、深度和广度，将速度列为熟悉的基础维度。本项目在此基础上整理出自动选法、提示词改写、执行与验收流程；速度维度的并行和迭代安排是本项目的扩展。项目对原文思想进行独立改编，引用原文并不代表 Felix Rieseberg 或 Anthropic 参与、认可或背书本项目。

Inspired by Felix Rieseberg’s [“How to be more ambitious: A tutorial for humans with models”](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/). This is an independent adaptation, not an endorsement by the author or Anthropic.

## 使用方式

- **直接交付任务**：技能适用时，先在内部优化，再执行并交付结果。简单任务采用轻量处理。
- **只改写**：说“只优化这个提示词，不执行：……”，获得可复制的提示词。
- **完整模式**：说“用完整版”，覆盖四个维度和深度方法。
- **跳过优化**：说“这次不优化，直接按原提示词执行”。

也可以显式调用：

```text
$ambitious-prompt 帮我规划一个月的产品试点，预算不超过 2 万元。
```

技能保留用户指定的时间、预算、资料范围和其他约束；把事实、推断与待验证项分开。模拟专家视角不等同于真实专家意见或外部评审。

## 安装

将仓库克隆到个人 Codex 技能目录：

```bash
git clone https://github.com/pearjelly/ambitious-prompt.git ~/.codex/skills/ambitious-prompt
```

如果该目录已存在，请先检查已有文件，避免覆盖。Codex 通常会自动发现新技能；未出现时可重启 Codex。技能允许自动调用，但是否选择某个技能仍取决于当前任务和环境。也可以在对话中用 `$ambitious-prompt` 显式调用。此项目此前名为 Task Compass 和 Prompt Upgrader；已安装旧版本的用户应迁移其个人设置，避免同时加载多个副本。

如希望直接给任务时默认使用它，可将以下约定加入个人 `~/.codex/AGENTS.md`：

```markdown
收到可执行任务时，使用 ambitious-prompt 先在内部优化，再完成用户授权的任务。简单任务保持简短。用户要求只改写时仅交付提示词；要求跳过优化时遵从。不要因此改变任务范围、约束或授权。
```

请保留已有的 `AGENTS.md` 内容，将约定追加到合适位置。更具体的用户要求和项目规则可能影响实际行为。参考 [Codex 全局指令文档](https://learn.chatgpt.com/docs/agent-configuration/agents-md)与 [Skills 文档](https://learn.chatgpt.com/docs/build-skills)。

## 文件结构

```text
SKILL.md                        触发条件、选法规则和输出方式
agents/openai.yaml              名称、示例与自动调用设置
references/methods.md           元升级及十种方法
references/evaluation-cases.md  行为回归案例
```

## 许可证

[MIT License](LICENSE)
