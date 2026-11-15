# Socratic Paper Writing 多平台原型 v0.1

本包是一份**离线适配初稿**，不会更改现有 GitHub 仓库，也没有发布或安装任何 Skill。

## 目录
- `core/WORKFLOW.md`：未来多个 AI 版本共同遵守的写作核心规范。
- `adapters/chatgpt/INSTRUCTIONS.md`：ChatGPT 项目指令或自定义 GPT 的指令草案。
- `tests/ACCEPTANCE.md`：跨平台行为验收清单。

## 如何在 ChatGPT 测试
1. 新建 ChatGPT 项目，名称自定，如 Socratic Paper Writing。
2. 将 `core/WORKFLOW.md` 上传为项目文件。
3. 把 `adapters/chatgpt/INSTRUCTIONS.md` 复制到项目指令中。
4. 新开一个聊天，发送“我不太会写课程论文，我先发老师的要求，你一步一步问我”。
5. 按 `tests/ACCEPTANCE.md` 测试边界条件。部分项目功能可能依套餐或客户端而异。

## 与原版对齐前不得直接替换
本稿依照公开仓库 README 的十步概要生成；尚未逐行核对原版 `socratic-paper-writing/SKILL.md` 的细节。下一步要逐条比对原版的具体提问模板、分支条件、核验规则、工具操作和边界约束，避免丢失原有能力。

## 维护规范
- 改核心逻辑：先改 `core/WORKFLOW.md`，再跑全部平台回归测试。
- 改平台用法：只改对应 `adapters/<platform>/`。
- 通过验收再发布；对用户公开标注支持平台、功能差异与限制。
