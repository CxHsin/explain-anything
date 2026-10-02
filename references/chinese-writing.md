# 中文写作

中文讲解使用本文件中的规则，并按内容选择强度：概念自然讲解，操作严谨。本地整理参考了 Fenng 的中文技术写作指南，并作教学用途的适配；不依赖另一个已安装技能，也不在每次使用时下载上游。

ASD-STE100 是英文技术文档的受控语言标准。这里借鉴减少歧义的方法，按中文句法处理表达；本文件和所参考的项目都不是 ASD-STE100 中文版，也不表示正式符合该标准。英文词表、词性、时态和句长限制不能直接移植到中文。

## 概念讲解

- 保持自然对话语气，可以直接称呼用户。用例子、类比和必要重复帮助理解；重复时补充新的角度，而非换一组同义词。
- 首次出现的关键术语、缩写或符号先解释，之后保持同一名称。采用用户或项目已经确定的术语，保留官方技术名称。
- 一句话保持一个清楚的主干；因果、条件和否定需要一起表达时保留完整关系，不为缩短句子拆散逻辑。不设中文句长硬阈值。
- 指代有歧义时写出具体对象。区分“现象”“原因”“推论”，保留结论的成立条件及适用范围。
- 类比应映射到真实概念，并说明必要的局限。抽象解释用具体例子落到结果，再回到一般关系；用户已有基础不必重讲。
- 去掉空泛修辞，写清实际含义；有明确定义的专业术语保持原样。选择性应用清晰写作规则，不把概念说明强制改成操作手册。

## 操作与故障排查

安装、配置、操作步骤及故障排查使用更完整的受控中文写作规则。在概念讲解里嵌入操作时，仅对该操作部分应用。

- 执行动作前必须知道的条件、限制和风险放在动作之前；有多个前提时先列明前置条件。
- 明确执行者与动作对象，区分用户操作和系统自动行为。需要顺序执行的多个动作拆成步骤；同时或不可分的操作保持在一起。
- 按实际执行顺序组织步骤。有依据时说明预期结果，帮助判断是否成功；提供来源支持的失败处理、停止条件或恢复方式。
- 故障排查先呈现可观察的现象与判断依据，再按证据价值和风险安排检查。可能原因保留为可能原因，证据足够时才作确定判断。
- 资料缺失时明确说明缺口，需要时先询问；不要补造命令、状态码、温度阈值、重试次数或恢复步骤。

## 事实与排版边界

以下规则适用于两类中文内容，事实和技术含义优先于语气与排版。

- 保留数字、单位、默认值、上下界、条件、例外、警告与失败处理；保持“可能”“通常”“建议”“计划”等词表达的确定程度。
- 区分来源事实与教学示例。可以为讲解构造明确标注的小例子，不能把自拟数值、假设或结论冒充来源内容。
- 改写后对照原文检查否定范围、条件范围和因果方向。已清楚的表达可以保留，不要求每句都换一种说法。
- 可编辑中文正文使用中文标点，中文与英文单词、缩写、阿拉伯数字及行内代码之间留一个普通半角空格；中文全角标点旁不额外加空格。
- 引号样式服从用户或项目约定；没有约定时沿用已有一致样式，新内容采用通常的中文引号即可，不强制切换为直角引号。
- 代码、命令、路径、URL、字段名、公式、固定引用及用户指定字面量保持准确。中英混合正文按中文规则处理外围排版，不修改标识符内部，不自动翻译技术名称。
- 同一概念的拼写和大小写优先遵循可靠来源或项目术语表。歧义词结合上下文判断，不做机械全局替换。

## 来源与适配说明

参考项目：[Fenng/Tech-Doc-Style-Chinese](https://github.com/Fenng/Tech-Doc-Style-Chinese)。固定来源提交为 [`726bb3e2cbb97cc6086533b410f46779d3c1028b`](https://github.com/Fenng/Tech-Doc-Style-Chinese/commit/726bb3e2cbb97cc6086533b410f46779d3c1028b)。

- [技能入口](https://github.com/Fenng/Tech-Doc-Style-Chinese/blob/726bb3e2cbb97cc6086533b410f46779d3c1028b/SKILL.md)：事实保真、规则优先级与按内容类型处理。
- [受控中文技术写作](https://github.com/Fenng/Tech-Doc-Style-Chinese/blob/726bb3e2cbb97cc6086533b410f46779d3c1028b/references/controlled-technical-chinese.md)：语言边界、规则强度、操作与故障排查。
- [术语与排版](https://github.com/Fenng/Tech-Doc-Style-Chinese/blob/726bb3e2cbb97cc6086533b410f46779d3c1028b/references/terminology-and-typography.md)：术语、中文标点与中西文留白。
- [上游 MIT 许可](https://github.com/Fenng/Tech-Doc-Style-Chinese/blob/726bb3e2cbb97cc6086533b410f46779d3c1028b/LICENSE)。

本技能只整理与理解任务相关的规则：允许自然称呼、类比和教学示例；引号按用户或项目约定处理。不引入产品文案流程、默认禁用第二人称、固定直角引号或源码段落换行要求。正式标准定位另参考 [ASD-STE100 官方说明](https://www.asd-ste100.org/about_STE.html) 与 [官方 FAQ](https://www.asd-ste100.org/STE_faq.html)。

## 上游版权与许可

```text
MIT License

Copyright (c) 2026 Fenng

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
