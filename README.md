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

### Additional Style Rules

The skill also includes these additional style rules:

- Prefer original IEEE Xplore BibTeX for IEEE journal and conference papers.
- Use Google Scholar BibTeX only when stronger publisher metadata is unavailable; use Google Books or publisher pages for textbooks.
- Protect common communications terms in titles, such as `{MIMO}`, `{OFDM}`, `{IoT}`, `{RIS}`, `{CSI}`, `{FedAvg}`, and `{Hybrid-FL}`.
- For IEEE early-access journal papers, do not invent final volume, issue, pages, month, or year. Use the IEEE Xplore Date of Publication and DOI in a `note` field, such as `note={early access, Feb. 24, 2026, doi: ...}`.
- Before citing an arXiv/preprint entry, check whether a formally published or peer-reviewed version exists.
- arXiv references use `@ARTICLE` in this project, with `journal={arXiv preprint:...}`. Include the base official arXiv identifier, such as `arXiv:2403.00561`, without version number or subject class unless the target venue asks for them. Do not include `note`, `url`, or `doi` for arXiv entries unless the target venue explicitly requires them.
- For textbooks, cite specific chapters or equations in LaTeX with locators such as `\cite[Ch. 2]{key}` or `\cite[Eq. (9.17)]{key}`.
- Unless the target venue explicitly requires a different rule, keep the first author and replace the rest with `and others` when there are more than 5 authors. If the target style requests it, use `UK` for United Kingdom conference locations and `United Arab Emirates` for UAE conference locations.

### How To Use With Codex

Install or copy this repository into your Codex skills directory, then invoke it explicitly or ask Codex to normalize or complete BibTeX references.

Example prompt:

```text
Use $bibtex-reference-normalizer to complete and standardize the following BibTeX references. Infer the target venue and style automatically.

[Paste BibTeX entries, paper titles, DOIs, or incomplete citations here]
```

### How To Use With Claude Code

Place this repository in your Claude Code workspace or copy `CLAUDE.md` / `AGENTS.md` into the target project. Claude Code can read `CLAUDE.md` as project instructions, while `AGENTS.md` provides the portable agent rules.

Example prompt:

```text
Follow CLAUDE.md and AGENTS.md to complete and normalize the following BibTeX references. Infer the target venue and style automatically.

[Paste BibTeX entries, paper titles, DOIs, or incomplete citations here]
```

### How To Use With Other Agents

Use `AGENTS.md` as the general instruction file for multi-agent systems, AI coding agents, or custom workflows. The rules are not tied to Codex-specific metadata.

Expected output:

1. Corrected complete BibTeX entries.
2. A short change note for each entry.
3. Source hints when metadata was searched or inferred.
4. `needs verification` labels for fields that cannot be reliably verified.

### Examples

#### Example 1: Fix an incorrectly formatted BibTeX entry

Input prompt:

```text
Use $bibtex-reference-normalizer to standardize this BibTeX entry. Infer the target venue and style automatically.

@article{9737334,
  author={Qi, Jiahao and Ma, Xiaoyu and Liu, Yuwen and Li, Qiang and Zhang, Kai and Chen, Wei and Wang, Lin},
  journal={IEEE Internet of Things Journal},
  title={High-quality model aggregation for Blockchain-Based Federated Learning via Reputation-Motivated Task Participation},
  year={2022},
  month={October},
  volume={9},
  number={19},
  pages={18378-18391},
  doi={10.1109/JIOT.2022.3157698}
}
```

Expected style of output:

```bibtex
@ARTICLE{9737334,
  author={Qi, Jiahao and others},
  journal={IEEE Internet Things J.},
  title={{H}igh-quality model aggregation for blockchain-based federated learning via reputation-motivated task participation},
  year={2022},
  month={Oct.},
  volume={9},
  number={19},
  pages={18378--18391},
  doi={10.1109/JIOT.2022.3157698}
}
```

Typical changes:

- Shortened authors because there are more than 5 authors.
- Abbreviated the IEEE journal name.
- Converted the title to sentence case and protected the first title letter.
- Converted `October` to `Oct.`.
- Replaced the page range hyphen with BibTeX double hyphens.

#### Example 2: Complete a reference from a title or partial metadata

Input prompt:

```text
Use $bibtex-reference-normalizer to complete and standardize this reference. Infer the target venue and style automatically.

Title: Survey on multi-task learning in smart transportation
Venue: IEEE Access
Year: 2024
```

Expected style of output after verification:

```bibtex
@ARTICLE{10401928,
  author={Alzahrani, Mohammed and Wang, Qianlong and Liao, Weixian and Chen, Xuhui and Yu, Wei},
  journal={IEEE Access},
  title={{S}urvey on multi-task learning in smart transportation},
  year={2024},
  volume={12},
  pages={17023--17044},
  doi={10.1109/ACCESS.2024.3355034}
}
```

Typical changes:

- Searched reliable sources using the title, venue, and year.
- Completed authors, volume, pages, and DOI.
- Kept `IEEE Access` unabridged.
- Did not add `month` or `number` for the IEEE Access entry.
- Added source hints or `needs verification` if any field could not be reliably verified.

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

### 补充格式规则

本 skill 还包含以下补充格式规则：

- IEEE 期刊和会议论文优先使用 IEEE Xplore 导出的原始 BibTeX。
- 只有在更强的出版社元数据不可用时，才使用 Google Scholar BibTeX；教材可参考 Google Books 或出版社页面。
- 标题中需要保护通信领域常见术语大小写，例如 `{MIMO}`、`{OFDM}`、`{IoT}`、`{RIS}`、`{CSI}`、`{FedAvg}`、`{Hybrid-FL}`。
- IEEE early-access 期刊论文不要编造最终卷号、期号、页码、月份或年份；用 IEEE Xplore 的 Date of Publication 和 DOI 写入 `note` 字段，例如 `note={early access, Feb. 24, 2026, doi: ...}`。
- 引用 arXiv/preprint 前，先检查是否已有正式发表或同行评议版本。
- 本项目中 arXiv 引用使用 `@ARTICLE`，并写成 `journal={arXiv preprint:...}`。引用应包含基础官方 arXiv identifier，例如 `arXiv:2403.00561`；默认不带版本号和学科分类，除非目标 venue 要求。除非目标 venue 明确要求，否则 arXiv 条目不添加 `note`、`url` 或 `doi`。
- 教材引用具体章节或公式时，在 LaTeX 引用命令中写定位信息，例如 `\cite[Ch. 2]{key}` 或 `\cite[Eq. (9.17)]{key}`。
- 除非目标 venue 明确要求其他规则，否则作者数量超过 5 个时保留第一作者并用 `and others` 表示其余作者。如果目标格式要求，英国会议地点写 `UK`；阿联酋会议地点写 `United Arab Emirates`。

### 如何在 Codex 中使用

将该仓库安装或复制到你的 Codex skills 目录中，然后显式调用它，或直接让 Codex 规范化/补全 BibTeX 引用。

示例 prompt：

```text
使用 $bibtex-reference-normalizer 完成和规范以下 BibTeX 参考文献，并自动推断目标场所和引用格式。

[在这里粘贴 BibTeX 条目、论文标题、DOI 或不完整引用]
```

### 如何在 Claude Code 中使用

将该仓库放到 Claude Code 工作区，或把 `CLAUDE.md` / `AGENTS.md` 复制到目标项目中。Claude Code 可以读取 `CLAUDE.md` 作为项目指令，`AGENTS.md` 则提供通用 agent 规则。

示例 prompt：

```text
使用 CLAUDE.md 和 AGENTS.md 完成和规范以下 BibTeX 参考文献，并自动推断目标场所和引用格式。

[在这里粘贴 BibTeX 条目、论文标题、DOI 或不完整引用]
```

### 如何在其他 Agent 或多智能体系统中使用

将 `AGENTS.md` 作为通用指令文件，用于多智能体系统、AI coding agent 或自定义工作流。这些规则不依赖 Codex 专有元数据。

期望输出：

1. 修改后的完整 BibTeX 条目。
2. 每条引用的简短修改说明。
3. 当元数据经过搜索或推断时，说明来源线索。
4. 对无法可靠核实的字段标注 `需核实`。

### 案例

#### 案例 1：修正格式错误的 BibTeX 条目

输入 prompt：

```text
使用 $bibtex-reference-normalizer 规范以下 BibTeX 条目，并自动推断目标场所和引用格式。

@article{9737334,
  author={Qi, Jiahao and Ma, Xiaoyu and Liu, Yuwen and Li, Qiang and Zhang, Kai and Chen, Wei and Wang, Lin},
  journal={IEEE Internet of Things Journal},
  title={High-quality model aggregation for Blockchain-Based Federated Learning via Reputation-Motivated Task Participation},
  year={2022},
  month={October},
  volume={9},
  number={19},
  pages={18378-18391},
  doi={10.1109/JIOT.2022.3157698}
}
```

期望输出风格：

```bibtex
@ARTICLE{9737334,
  author={Qi, Jiahao and others},
  journal={IEEE Internet Things J.},
  title={{H}igh-quality model aggregation for blockchain-based federated learning via reputation-motivated task participation},
  year={2022},
  month={Oct.},
  volume={9},
  number={19},
  pages={18378--18391},
  doi={10.1109/JIOT.2022.3157698}
}
```

典型修改：

- 作者数量超过 5 个，保留第一作者并使用 `and others`。
- 将 IEEE 期刊名改为官方缩写。
- 将标题改为 sentence case，并保护标题首字母。
- 将 `October` 改为 `Oct.`。
- 将页码范围改为 BibTeX 双连字符。

#### 案例 2：根据标题或部分信息自动补全文献

输入 prompt：

```text
使用 $bibtex-reference-normalizer 完成和规范以下 BibTeX 参考文献，并自动推断目标场所和引用格式。

Title: Survey on multi-task learning in smart transportation
Venue: IEEE Access
Year: 2024
```

核实后期望输出风格：

```bibtex
@ARTICLE{10401928,
  author={Alzahrani, Mohammed and Wang, Qianlong and Liao, Weixian and Chen, Xuhui and Yu, Wei},
  journal={IEEE Access},
  title={{S}urvey on multi-task learning in smart transportation},
  year={2024},
  volume={12},
  pages={17023--17044},
  doi={10.1109/ACCESS.2024.3355034}
}
```

典型修改：

- 根据标题、venue 和年份搜索可靠来源。
- 补全作者、卷号、页码和 DOI。
- 保持 `IEEE Access` 不缩写。
- 不为 IEEE Access 条目添加 `month` 或 `number`。
- 如果字段无法可靠核实，应说明来源线索或标注 `需核实`。

### 文件结构

```text
SKILL.md              # Codex skill 指令
agents/openai.yaml    # Codex UI 元数据
AGENTS.md             # 面向 AI agents 和多智能体系统的通用指令
CLAUDE.md             # Claude Code 项目指令
README.md             # 中英双语项目说明
```
