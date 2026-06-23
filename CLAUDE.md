# Claude Code Instructions

Use this repository as a BibTeX reference normalization skill for computer science and communications papers.

Read and follow `AGENTS.md` for the portable agent instructions. Read `SKILL.md` for the Codex skill version of the same rules.

When the user asks Claude Code to normalize references:

1. Identify the target style: IEEE by default, ACM when the venue or entry clearly requires ACM Reference Format.
2. Return corrected complete BibTeX entries.
3. Add short change notes.
4. Use `needs verification` for uncertain metadata in English responses and `需核实` in Chinese responses.
5. Do not invent missing bibliographic metadata.

For implementation details, follow the rules in `AGENTS.md` exactly.

# Claude Code 使用说明

本仓库可作为计算机与通信领域 BibTeX 引用规范化的 Claude Code 指令库。

请优先阅读并遵循 `AGENTS.md` 中的通用 agent 指令；`SKILL.md` 是同一套规则的 Codex skill 版本。

当用户要求 Claude Code 规范化参考文献时：

1. 判断目标格式：默认使用 IEEE；若目标会议/期刊或条目明显要求 ACM Reference Format，则使用 ACM。
2. 输出修改后的完整 BibTeX 条目。
3. 添加简短修改说明。
4. 英文回答中用 `needs verification` 标注无法确认的信息，中文回答中用 `需核实`。
5. 不要编造缺失的文献信息。

具体规则严格遵循 `AGENTS.md`。
