# BibTeX Reference Normalizer

## English

`bibtex-reference-normalizer` is a reusable instruction set for normalizing and completing BibTeX references in computer science and communications papers. It includes a Codex skill format and portable agent instructions for tools such as Claude Code and other AI coding agents. It focuses on IEEE-style journal and conference references, IEEE Access entries, ACM references, and arXiv/preprint entries.

### What This Project Does

- Standardizes BibTeX fields for IEEE journals, IEEE conferences, ACM publications, and arXiv entries.
- Completes missing BibTeX metadata from partial inputs such as paper titles, DOIs, arXiv IDs, partial author lists, venue names, or incomplete citations when reliable web access is available.
- Applies IEEE-style author truncation rules when appropriate.
- Normalizes title capitalization with BibTeX brace protection.
- Handles IEEE Access entries without adding unnecessary `month` or `number` fields.
- Formats IEEE conference locations, including special formats for the USA, U.K., and U.A.E.
- Preserves important metadata such as DOI, URL, pages, volume, publisher, series, and article number.
- Marks uncertain metadata as `needs verification` instead of inventing missing information.

### Metadata Completion Policy

When only partial information is provided, the agent should search authoritative sources first: DOI/Crossref, publisher pages, IEEE Xplore, ACM Digital Library, arXiv, DBLP, and official venue pages. Secondary sources such as Semantic Scholar, OpenAlex, Google Scholar snippets, or general web search should be used only as supporting evidence. If multiple plausible records exist, the agent should ask for clarification or mark ambiguous fields as `needs verification`.

### How To Use With Codex

Install or copy this repository into your Codex skills directory, then invoke it explicitly or ask Codex to normalize or complete BibTeX references.

Example prompt:

```text
Use $bibtex-reference-normalizer to complete and standardize the following BibTeX references for an IEEE paper.

[Paste BibTeX entries, paper titles, DOIs, or incomplete citations here]
```

### How To Use With Claude Code

Place this repository in your Claude Code workspace or copy `CLAUDE.md` / `AGENTS.md` into the target project. Claude Code can read `CLAUDE.md` as project instructions, while `AGENTS.md` provides the portable agent rules.

Example prompt:

```text
Follow CLAUDE.md and AGENTS.md to complete and normalize the following BibTeX references for an IEEE paper.

[Paste BibTeX entries, paper titles, DOIs, or incomplete citations here]
```

### How To Use With Other Agents

Use `AGENTS.md` as the general instruction file for multi-agent systems, AI coding agents, or custom workflows. The rules are not tied to Codex-specific metadata.

Expected output:

1. Corrected complete BibTeX entries.
2. A short change note for each entry.
3. Source hints when metadata was searched or inferred.
4. `needs verification` labels for fields that cannot be reliably verified.

### File Structure

```text
SKILL.md              # Codex skill instructions
agents/openai.yaml    # Codex UI metadata
AGENTS.md             # Portable instructions for AI agents and multi-agent systems
CLAUDE.md             # Claude Code project instructions
README.md             # Bilingual project documentation
```

## 中文

`bibtex-reference-normalizer` 是一套可复用的 BibTeX 引用规范化与补全指令，主要面向计算机与通信领域论文。它既包含 Codex skill 格式，也包含适用于 Claude Code 和其他 AI coding agents 的通用 agent 指令。它重点支持 IEEE 期刊、IEEE 会议、IEEE Access、ACM 出版物以及 arXiv/预印本条目。

### 这个项目的作用

- 规范 IEEE 期刊、IEEE 会议、ACM 出版物和 arXiv 条目的 BibTeX 字段。
- 当具备可靠联网能力时，可根据论文标题、DOI、arXiv ID、部分作者、会议/期刊名或不完整引用补全文献信息。
- 根据 IEEE 风格处理作者数量较多时的缩写规则。
- 规范标题的 sentence case，并用 BibTeX 大括号保护必要的大写字母。
- 对 IEEE Access 条目避免添加不必要的 `month` 和 `number` 字段。
- 规范 IEEE 会议地点格式，包括美国、英国和阿联酋的特殊写法。
- 保留 DOI、URL、页码、卷号、出版社、会议系列、article number 等重要元数据。
- 对无法可靠确认的信息标注 `需核实`，不编造缺失信息。

### 元数据补全原则

当用户只提供部分信息时，agent 应优先搜索权威来源：DOI/Crossref、出版社页面、IEEE Xplore、ACM Digital Library、arXiv、DBLP 和官方会议/期刊页面。Semantic Scholar、OpenAlex、Google Scholar 摘要或普通网页只作为辅助证据。如果存在多个可能记录，应要求用户确认，或将有歧义字段标注为 `需核实`。

### 如何在 Codex 中使用

将该仓库安装或复制到你的 Codex skills 目录中，然后显式调用它，或直接让 Codex 规范化/补全 BibTeX 引用。

示例 prompt：

```text
Use $bibtex-reference-normalizer to complete and standardize the following BibTeX references for an IEEE paper.

[在这里粘贴 BibTeX 条目、论文标题、DOI 或不完整引用]
```

### 如何在 Claude Code 中使用

将该仓库放到 Claude Code 工作区，或把 `CLAUDE.md` / `AGENTS.md` 复制到目标项目中。Claude Code 可以读取 `CLAUDE.md` 作为项目指令，`AGENTS.md` 则提供通用 agent 规则。

示例 prompt：

```text
Follow CLAUDE.md and AGENTS.md to complete and normalize the following BibTeX references for an IEEE paper.

[在这里粘贴 BibTeX 条目、论文标题、DOI 或不完整引用]
```

### 如何在其他 Agent 或多智能体系统中使用

将 `AGENTS.md` 作为通用指令文件，用于多智能体系统、AI coding agent 或自定义工作流。这些规则不依赖 Codex 专有元数据。

期望输出：

1. 修改后的完整 BibTeX 条目。
2. 每条引用的简短修改说明。
3. 当元数据经过搜索或推断时，说明来源线索。
4. 对无法可靠核实的字段标注 `需核实`。

### 文件结构

```text
SKILL.md              # Codex skill 指令
agents/openai.yaml    # Codex UI 元数据
AGENTS.md             # 面向 AI agents 和多智能体系统的通用指令
CLAUDE.md             # Claude Code 项目指令
README.md             # 中英双语项目说明
```
