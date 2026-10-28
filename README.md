# Ambitious Prompt

一个面向支持 [Agent Skills](https://agentskills.io/specification) 的 AI 工具的提示词优化 Skill。用户手动调用后，它根据任务，从高度、广度、深度、速度四个维度选择适用方法，明确目标、约束、证据和验收标准，生成可复制的提示词。

Ambitious Prompt is a manually invoked Agent Skill that adapts prompt improvement methods to each task. It returns a reusable prompt by default and executes only when explicitly requested. Previously named Task Compass and Prompt Upgrader.

## 方法来源

本项目的核心框架受到 Felix Rieseberg 的文章 [《How to be more ambitious: A tutorial for humans with models》](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/) 启发。Felix 是 Anthropic 的工程经理，曾负责 Claude.ai、Cowork 和 Claude Code Desktop 的工程工作。他在文中提出用四个维度思考如何更有野心地使用 AI：

- **高度（Altitude）**：关注任务背后想达到的结果。
- **广度（Range）**：引入不同领域的知识、工具和方法。
- **深度（Depth）**：运用专业方法、原始数据和外部检验，把问题做深。
- **速度（Speed）**：用更少时间完成工作。

原文重点展开高度、深度和广度，将速度列为熟悉的基础维度。本项目在此基础上整理出自动选法、提示词改写、执行与验收流程；速度维度的并行和迭代安排是本项目的扩展。项目对原文思想进行独立改编，引用原文并不代表 Felix Rieseberg 或 Anthropic 参与、认可或背书本项目。

Inspired by Felix Rieseberg’s [“How to be more ambitious: A tutorial for humans with models”](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/). This is an independent adaptation, not an endorsement by the author or Anthropic.

## 使用方式

- **手动改写**：调用本技能并给出任务，默认获得可复制的提示词。
- **改写并执行**：调用技能时明确说“改写后执行”，再完成用户授权的任务。
- **完整模式**：说“用完整版”，覆盖四个维度和深度方法。

例如，在 Codex 中也可以显式调用：

```text
$ambitious-prompt 只改写提示词：帮我规划一个月的产品试点，预算不超过 2 万元。
```

技能保留用户指定的时间、预算、资料范围和其他约束；把事实、推断与待验证项分开。模拟专家视角不等同于真实专家意见或外部评审。

## 安装

将仓库克隆到所用工具的个人技能目录，保留 `SKILL.md` 和 `references/` 的相对位置。选择与你使用的工具对应的一组命令即可；目标目录已存在时先检查并备份，避免覆盖。

**Codex**：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/pearjelly/ambitious-prompt.git ~/.codex/skills/ambitious-prompt
```

**Claude Code**：

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/pearjelly/ambitious-prompt.git ~/.claude/skills/ambitious-prompt
```

**OpenCode**：

```bash
mkdir -p ~/.config/opencode/skills
git clone https://github.com/pearjelly/ambitious-prompt.git ~/.config/opencode/skills/ambitious-prompt
```

其他支持 Agent Skills 的工具可按其官方文档安装此目录。`agents/openai.yaml` 是 Codex 的可选界面配置；核心规则和方法库不依赖它。此项目此前名为 Task Compass 和 Prompt Upgrader；已安装旧版本的用户应迁移其个人设置，避免同时加载多个副本。

## 设置手动调用

- **Codex**：本技能已通过 `agents/openai.yaml` 关闭隐式调用。使用 `$ambitious-prompt` 显式调用。
- **Claude Code**：安装后，在该工具的技能副本的 `SKILL.md` 顶部 YAML 中加入 `disable-model-invocation: true`，然后通过 `/ambitious-prompt` 调用。该字段是 Claude Code 的扩展；请勿添加到同时供 Codex 验证的同一份技能副本中。
- **OpenCode V2**：在该工具的技能副本的 `SKILL.md` 顶部 YAML 中加入 `metadata:` 及其下缩进的 `opencode/autoinvoke: false`，然后使用 `@ambitious-prompt` 调用。V1 文档未提供同等的隐式调用关闭设置；描述中的“仅手动”只是指令，不能保证自动触发被禁用，请确认所用版本支持相应设置后再安装。
- **其他工具**：按其官方文档关闭模型自动调用。若工具没有此功能，技能的文字描述无法提供强制保证。

如果此前曾在个人或项目指令文件中加入自动调用本技能的规则，请自行删除对应规则并保留其他内容。安装和调用机制参考 [Codex Skills](https://learn.chatgpt.com/docs/build-skills)、[Claude Code Skills](https://code.claude.com/docs/en/skills) 和 [OpenCode Skills V2](https://opencode.ai/v2/docs/skills)。

## 文件结构

```text
SKILL.md                        触发条件、选法规则和输出方式
agents/openai.yaml              Codex 名称、示例与手动调用设置
references/methods.md           元升级及十种方法
references/evaluation-cases.md  行为回归案例
```

## 许可证

[MIT License](LICENSE)
