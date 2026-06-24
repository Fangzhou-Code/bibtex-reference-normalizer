# Claude Code Instructions

Use this repository as a BibTeX reference normalization and completion skill for computer science and communications papers.

Read and follow `AGENTS.md` for the portable agent instructions. Read `SKILL.md` for the Codex skill version of the same rules.

When the user asks Claude Code to normalize or complete references:

1. Infer the target venue and style from the reference metadata, DOI, arXiv ID, publisher page, IEEE Xplore, ACM Digital Library, DBLP, Crossref, or official venue page. Default to IEEE only if the style remains unclear and the entry is in the computer science or communications domain.
2. If only partial metadata is provided, such as a title, DOI, arXiv ID, partial author list, or incomplete citation, search reliable sources when internet access is available.
3. Build the BibTeX entry only from verified metadata.
4. Return corrected complete BibTeX entries.
5. Add short change notes and source hints.
6. Use `needs verification` for uncertain metadata in English responses and `需核实` in Chinese responses.
7. Do not invent missing bibliographic metadata.

For implementation details, follow the rules in `AGENTS.md` exactly.

# Claude Code 使用说明

本仓库可作为计算机与通信领域 BibTeX 引用规范化与补全的 Claude Code 指令库。

请优先阅读并遵循 `AGENTS.md` 中的通用 agent 指令；`SKILL.md` 是同一套规则的 Codex skill 版本。

当用户要求 Claude Code 规范化或补全参考文献时：

1. 根据引用元数据、DOI、arXiv ID、出版社页面、IEEE Xplore、ACM Digital Library、DBLP、Crossref 或官方 venue 页面自动推断目标场所和引用格式。只有当格式仍不清楚且条目属于计算机或通信领域时，才默认使用 IEEE。
2. 如果用户只提供标题、DOI、arXiv ID、部分作者或不完整引用，在具备联网能力时搜索可靠来源。
3. 只使用已核实的元数据构造 BibTeX 条目。
4. 输出修改后的完整 BibTeX 条目。
5. 添加简短修改说明和来源线索。
6. 英文回答中用 `needs verification` 标注无法确认的信息，中文回答中用 `需核实`。
7. 不要编造缺失的文献信息。

具体规则严格遵循 `AGENTS.md`。
