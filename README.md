# Explain Anything

一个帮助理解具体问题或材料的 Agent Skill：根据卡住的位置，选择清晰文字、图解或交互演示。默认中文，优先在对话内呈现，也支持英文和用户指定的形式。

输入可以是一个概念、一段文字、一个链接、一篇论文，或对上一条回答的追问。目标是看清关键关系与过程，保留原始事实、条件和技术含义。

## 如何选择解释形式

| 卡住的位置 | 优先形式 | 示例 |
| --- | --- | --- |
| 术语、定义、概念区别 | 文字，必要时用小表格 | 梯度和学习率有什么区别？ |
| 结构、步骤、依赖、因果关系 | 图解 | 浏览器请求怎样到达数据库？ |
| 参数变化、动态过程、计算迭代 | 交互演示 | 学习率变大后，为什么会振荡或发散？ |

用户指定的形式优先。普通事实查询保持简洁，不自动扩展成教学网页。说“还是没懂”时，技能会结合反馈定位剩余困惑，再换例子、粒度或表达形式；关键信息不足时先询问。

当前覆盖文字、静态图解和交互演示，不包含视频制作，也不自动建立长期课程或学习档案。

## 安装与使用

需要支持本地 Skills 的 Agent。选择下面一种安装方式；已有安装时，先检查并保留本地修改，避免直接覆盖。

### 通过 npx 安装

需要 Node.js/npm。按使用的 Agent 选择命令，安装到用户级目录，并保留安装过程中的交互确认。这些 npx 命令可用于 Windows、macOS 和 Linux。

**Codex**

```bash
npx skills add https://github.com/CxHsin/explain-anything --skill explain-anything -a codex -g
```

**Claude Code**

```bash
npx skills add https://github.com/CxHsin/explain-anything --skill explain-anything -a claude-code -g
```

**Cursor**

```bash
npx skills add https://github.com/CxHsin/explain-anything --skill explain-anything -a cursor -g
```

**OpenCode**

```bash
npx skills add https://github.com/CxHsin/explain-anything --skill explain-anything -a opencode -g
```

`--skill explain-anything` 指定技能，`-a` 指定 Agent，`-g` 表示用户级安装；去掉 `-g` 可安装到当前项目。其他 Agent 的名称与安装选项见 [skills CLI 官方说明](https://github.com/vercel-labs/skills#install-a-skill)。

| Agent | `-a` 参数 | 默认用户级目录 |
| --- | --- | --- |
| Codex | `codex` | `~/.codex/skills/` |
| Claude Code | `claude-code` | `~/.claude/skills/` |
| Cursor | `cursor` | `~/.cursor/skills/` |
| OpenCode | `opencode` | `~/.config/opencode/skills/` |

`~` 表示用户主目录，实际路径以安装工具和环境配置为准。各 Agent 的技能加载和显式调用方式可能不同；下面的 `$explain-anything` 示例以 Codex 为例。对话内交互演示还取决于宿主能力，安装技能本身不会增加渲染工具。

### 让 Agent 安装

将下面这段话复制给 Codex、Claude Code、Cursor、OpenCode 或其他具备文件操作和安装能力的 Agent，由它根据当前平台选择目录：

```text
请从 https://github.com/CxHsin/explain-anything 安装 explain-anything 技能到当前 Agent 的用户级技能目录。先检查是否已有安装；如果存在，保留本地修改，不直接覆盖。安装完整技能目录，包含 references 和 agents 文件，并确认 SKILL.md 可读取。完成后告诉我如何调用。
```

### 手动安装

需要 Git，以及支持本地 Skills 的 Agent。下面将仓库安装到 Codex 的用户级技能目录；设置了 `CODEX_HOME` 时使用该目录，否则使用 `~/.codex`。

下面的手动安装脚本遇到已有 `explain-anything` 目录时会停止安装，不覆盖现有目录；已有 Git 克隆可在确认工作区干净后更新。

#### Windows PowerShell

```powershell
$skillHome = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $HOME '.codex' }
$skillDir = Join-Path $skillHome 'skills/explain-anything'
if (Test-Path -LiteralPath $skillDir) { throw 'explain-anything 已存在，请先检查本地版本。' }
New-Item -ItemType Directory -Force -Path (Split-Path -Parent $skillDir) | Out-Null
git clone https://github.com/CxHsin/explain-anything.git $skillDir
```

#### macOS / Linux

```bash
skill_dir="${CODEX_HOME:-$HOME/.codex}/skills/explain-anything"
if [ -e "$skill_dir" ]; then
  echo 'explain-anything 已存在，请先检查本地版本。'
else
  mkdir -p "$(dirname "$skill_dir")"
  git clone https://github.com/CxHsin/explain-anything.git "$skill_dir"
fi
```

### 使用示例

安装完成后，让 Agent 重新加载技能列表；必要时重新打开应用或会话。确认技能可见后，显式调用：

```text
$explain-anything 我懂导数，但没理解学习率为什么会影响收敛，请选择合适的形式解释。
```

也可以指定形式或提供材料：

```text
$explain-anything 用图解释浏览器请求怎样到达数据库。
$explain-anything 只用文字解释下面这段论文，保留公式的成立条件：……
$explain-anything 我还是没懂为什么沿负梯度更新，请换一个例子。
```

技能保留自动发现配置，供宿主在相关理解任务中选择使用。图解可直接使用 Mermaid；对话内交互演示按需使用环境中的 `visualize` 技能。缺少对话内交互能力时，提供独立 HTML；能否生成文件、运行和验证演示取决于宿主工具，未执行的检查会明确说明。

## 思想来源：Karpathy 的 X 帖子

本技能受到 [Andrej Karpathy 这篇 X 帖子](https://x.com/karpathy/status/2105819303471976479) 的启发。

帖子的核心思路是：随着语言模型承担更多工作，人需要理解与检查模型的输出；模型也可以帮助完成这种理解。除了文字，可以按需生成图解、交互网页，甚至定制讲解视频。这些针对当前问题制作的工具，即使只使用一次，也可能有价值。

本项目将这一思路整理为可复用的解释流程：先识别理解障碍，再选择合适的形式，最后核对来源、例子和演示。形式根据问题选择，并不要求每次都升级为更复杂的媒体。视频属于原帖讨论的方向，当前技能尚未实现。

## 中文规则借鉴与语言分工

中文写作规则参考了 [Fenng/Tech-Doc-Style-Chinese](https://github.com/Fenng/Tech-Doc-Style-Chinese)，固定参考提交为 [`726bb3e2cbb97cc6086533b410f46779d3c1028b`](https://github.com/Fenng/Tech-Doc-Style-Chinese/commit/726bb3e2cbb97cc6086533b410f46779d3c1028b)。主要借鉴：

- 保留事实、条件、限制、单位和不确定程度。
- 保持术语一致、指代明确，条件和风险先于操作。
- 按内容选择规则强度，并保护代码、命令、路径和固定引用。
- 处理中文标点与中英文留白。

本技能作了教学适配：概念解释保留自然对话、类比和必要重复；操作与故障排查采用更严谨的步骤表达。引号样式遵循用户或项目约定，不强制使用直角引号，也不引入上游产品文案流程。完整来源与适配说明见 [中文写作参考](references/chinese-writing.md)。

[ASD-STE100](https://www.asd-ste100.org/about_STE.html) 是英文技术文档的受控语言标准。英文解释参考其清晰写作原则；中文按中文句法采用整理后的规则。Fenng 项目和本技能都不是 ASD-STE100 的中文版本，也不宣称正式符合该标准。

以上属于思想启发和规则借鉴，不表示 Karpathy、Fenng 或 ASD-STE100 的维护者参与或背书本项目。

## 文件结构

```text
explain-anything/
├── SKILL.md
├── README.md
├── LICENSE
├── agents/
│   └── openai.yaml
└── references/
    ├── chinese-writing.md
    └── formats.md
```

[SKILL.md](SKILL.md) 是技能入口；[格式指导](references/formats.md) 提供文字、图解和交互演示的处理方式。项目不包含 API 密钥、上游检查脚本或固定演示模板。

## 许可证

本项目采用 [MIT License](LICENSE)，项目版权为 `Copyright (c) 2026 CxHsin`。

借鉴 Fenng 项目的中文规则适用其原有 MIT 许可；[中文写作参考](references/chinese-writing.md#上游版权与许可) 保留了 `Copyright (c) 2026 Fenng` 和完整许可文本。使用、修改或分发相关内容时，应保留适用的版权与许可声明。

对 Karpathy 原帖和 ASD-STE100 官方资料的链接用于说明思想与标准背景，项目 MIT 许可不替代这些外部资料自身的权利或许可。
