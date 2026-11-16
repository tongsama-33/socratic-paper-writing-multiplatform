# Socratic Paper Writing 多平台原型 v0.1

本仓库是一份 **ChatGPT / Gemini 多平台适配原型**，包含共享写作流程与平台指令。当前为待实测初稿，尚未发布可一键安装的 Skill；原版仓库保持独立。

## 目录
- `core/WORKFLOW.md`：未来多个 AI 版本共同遵守的写作核心规范。
- `adapters/chatgpt/INSTRUCTIONS.md`：ChatGPT 项目指令或自定义 GPT 的指令草案。
- `adapters/gemini/INSTRUCTIONS.md`：Gemini Gems 或对话式环境的指令草案。
- `tests/ACCEPTANCE.md`：跨平台行为验收清单。

## 如何在 ChatGPT 测试
1. 新建 ChatGPT 项目，名称自定，如 Socratic Paper Writing。
2. 将 `core/WORKFLOW.md` 上传为项目文件。
3. 把 `adapters/chatgpt/INSTRUCTIONS.md` 复制到项目指令中。
4. 新开一个聊天，发送“我不太会写课程论文，我先发老师的要求，你一步一步问我”。
5. 按 `tests/ACCEPTANCE.md` 测试边界条件。部分项目功能可能依套餐或客户端而异。

## 如何在 Gemini 测试
1. 打开 Gemini 网页端，从侧栏进入 Gems 并选择新建（入口名称可能随账号和界面更新变化），名称自定，如 Socratic Paper Writing。
2. 将 `core/WORKFLOW.md` 上传为知识库文件（Knowledge）。
3. 把 `adapters/gemini/INSTRUCTIONS.md` 复制到指令（Instructions）框中并保存。
4. 新开一个聊天，发送“我不太会写课程论文，我先发老师的要求，你一步一步问我”。
5. 按 `tests/ACCEPTANCE.md` 测试边界条件，另外检查：无法联网时不声称已检索；缺少共享文件时提示简版限制；只读摘要时不声称全文核验；无法生成文件时提供可复制文本；新对话通过状态卡恢复。

如果无法创建 Gem，可在普通 Gemini 对话中上传或粘贴 `core/WORKFLOW.md`，再粘贴 Gemini 指令开始测试。若无法读取 Markdown，可粘贴纯文本。Google 正在调整 Gems 功能与入口，请以当前账号界面为准；本仓库尚未验证新入口的安装兼容性。

## 能力与测试边界
- 联网、上传、导出和上下文能力以当前账号、地区与客户端实际提供的功能为准，指令本身不会赋予工具权限。
- 搜索结果和自动生成的引用仍需逐条核查；元数据正确不代表论文结论获得支持。
- 目前完成指令内容检查，尚未完成 ChatGPT / Gemini 的端到端实测，不承诺与原版功能完全一致。
- Gemini 设置与知识文件用法参考：[Google 官方帮助](https://support.google.com/gemini/answer/15146780?hl=zh-Hans)（核对日期：2026-11-16）。

## 与原版对齐前不得直接替换
本稿依照公开仓库 README 的十步概要生成；尚未逐行核对原版 `socratic-paper-writing/SKILL.md` 的细节。下一步要逐条比对原版的具体提问模板、分支条件、核验规则、工具操作和边界约束，避免丢失原有能力。

## 维护规范
- 改核心逻辑：先改 `core/WORKFLOW.md`，再跑全部平台回归测试。
- 改平台用法：只改对应 `adapters/<platform>/`。
- 通过验收再发布；对用户公开标注支持平台、功能差异与限制。
