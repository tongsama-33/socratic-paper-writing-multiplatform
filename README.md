# Socratic Paper Writing 多平台原型 v0.2

本仓库是一份 **ChatGPT / Gemini 多平台适配原型**，包含共享写作流程与平台指令。当前为待实测初稿，尚未发布可一键安装的 Skill；原版仓库保持独立。

## 目录
- `core/WORKFLOW.md`：未来多个 AI 版本共同遵守的写作核心规范。
- `adapters/chatgpt/INSTRUCTIONS.md`：ChatGPT 项目指令或自定义 GPT 的指令草案。
- `adapters/gemini/INSTRUCTIONS.md`：Gemini 网页版与 App 的 Gem 指令，配合共享工作流使用。
- `adapters/gemini/GEMINI.md`：Gemini CLI 项目上下文分发模板。
- `adapters/gemini/STANDALONE_PROMPT.md`：内嵌完整共享流程的单文件粘贴版。
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

## Gemini CLI 本地使用
1. 在本地准备一个论文项目文件夹。
2. 将 `adapters/gemini/GEMINI.md` 复制到该文件夹根目录，保留文件名 `GEMINI.md`。已有同名文件时合并规则并保留原内容。
3. 将 `core/WORKFLOW.md` 复制到同一目录，保留文件名 `WORKFLOW.md`。模板通过 `@./WORKFLOW.md` 导入共享流程；不要只把模板留在仓库适配器目录并假设它会定位论文文件。
4. 在论文项目目录启动已安装并配置好的 Gemini CLI。输入 `/memory show`，确认包含“产品目标”“全局约束”“10 个阶段”等完整流程；必要时使用 `/memory reload` 或重启会话。命令名称以当前 CLI 帮助为准。
5. 告诉 CLI 要处理的课程要求与文件路径。Markdown 和纯文本按权限读写；Word、PDF 等格式需要对应工具。修改前保留原稿，修改后重新读取核验，工具不足时交付可复制文本。
6. 若出现导入失败，检查两个文件是否同目录、文件名是否正确，以及工作区访问权限。补齐前不得声称已加载完整流程。

此模板导入规则依据 [Gemini CLI 官方上下文文档](https://geminicli.com/docs/cli/gemini-md/) 与 [导入文档](https://geminicli.com/docs/reference/memport/)（核对日期：2026-11-16）。指令文件本身不会授予文件系统权限。

## 单文件粘贴使用
1. 打开 `adapters/gemini/STANDALONE_PROMPT.md`，复制完整正文，粘贴到新的 Gemini 对话或其他支持长文本指令的客户端。
2. 再发送课程要求和已有材料。本文件已经包含共享流程，无需另传 `WORKFLOW.md`。
3. 如客户端长度限制导致截断，不要假设已加载完整内容；改用支持完整输入的客户端，或使用共享文件加平台指令的方式。
4. 新对话需要重新粘贴单文件指令和状态卡。兼容其他客户端仅指文本使用方式，联网、文件操作及指令遵循能力仍需逐一实测。

## 能力与测试边界
- 联网、上传、导出和上下文能力以当前账号、地区与客户端实际提供的功能为准，指令本身不会赋予工具权限。
- 搜索结果和自动生成的引用仍需逐条核查；元数据正确不代表论文结论获得支持。
- 目前完成指令内容检查，尚未完成 ChatGPT / Gemini 的端到端实测，不承诺与原版功能完全一致。
- Gemini 设置与知识文件用法参考：[Google 官方帮助](https://support.google.com/gemini/answer/15146780?hl=zh-Hans)（核对日期：2026-11-16）。

## 与原版对齐前不得直接替换
本稿依照公开仓库 README 的十步概要生成；尚未逐行核对原版 `socratic-paper-writing/SKILL.md` 的细节。下一步要逐条比对原版的具体提问模板、分支条件、核验规则、工具操作和边界约束，避免丢失原有能力。

## 维护规范
- 改核心逻辑：先改 `core/WORKFLOW.md`，再跑全部平台回归测试。
- 改平台用法：修改对应 `adapters/<platform>/`，并检查所有派生入口。
- 共享规范以 `core/WORKFLOW.md` 为准。单文件版按“完整 WORKFLOW + Gemini 指令”合并生成；只替换外部加载提示与跨对话恢复措辞，不手工另写一套核心规则。
- 任一来源变化后重新合并单文件版，更新其来源版本与日期，确认十阶段、全局约束与证据边界均保留。
- CLI 使用独立文件操作规则，不导入网页版关于本地磁盘的限制。分发前检查同目录导入路径及来源一致性。
- v0.2 新增 CLI 与单文件入口；核心流程仍为 v0.1。内容检查通过不代表实际客户端验收通过。
- 通过验收再发布；对用户公开标注支持平台、功能差异与限制。
