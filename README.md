# BibTeX Reference Normalizer

## English

`bibtex-reference-normalizer` is a Codex skill for normalizing BibTeX references in computer science and communications papers. It focuses on IEEE-style journal and conference references, IEEE Access entries, ACM references, and arXiv/preprint entries.

### What This Skill Does

- Standardizes BibTeX fields for IEEE journals, IEEE conferences, ACM publications, and arXiv entries.
- Applies IEEE-style author truncation rules when appropriate.
- Normalizes title capitalization with BibTeX brace protection.
- Handles IEEE Access entries without adding unnecessary `month` or `number` fields.
- Formats IEEE conference locations, including special formats for the USA, U.K., and U.A.E.
- Preserves important metadata such as DOI, URL, pages, volume, publisher, series, and article number.
- Marks uncertain metadata as `需核实` instead of inventing missing information.

### How To Use

Install or copy this skill into your Codex skills directory, then invoke it explicitly or ask Codex to normalize BibTeX references.

Example prompt:

```text
Use $bibtex-reference-normalizer to standardize the following BibTeX references for an IEEE paper.

[Paste BibTeX entries here]
```

Expected output:

1. Corrected complete BibTeX entries.
2. A short change note for each entry.
3. `需核实` labels for fields that cannot be reliably verified.

### Skill Files

```text
SKILL.md
agents/openai.yaml
```

`SKILL.md` contains the normalization rules. `agents/openai.yaml` provides Codex UI metadata.

## 中文

`bibtex-reference-normalizer` 是一个用于规范化 BibTeX 引用的 Codex skill，主要面向计算机与通信领域论文。它重点支持 IEEE 期刊、IEEE 会议、IEEE Access、ACM 出版物以及 arXiv/预印本条目。

### 这个 Skill 的作用

- 规范 IEEE 期刊、IEEE 会议、ACM 出版物和 arXiv 条目的 BibTeX 字段。
- 根据 IEEE 风格处理作者数量较多时的缩写规则。
- 规范标题的 sentence case，并用 BibTeX 大括号保护必要的大写字母。
- 对 IEEE Access 条目避免添加不必要的 `month` 和 `number` 字段。
- 规范 IEEE 会议地点格式，包括美国、英国和阿联酋的特殊写法。
- 保留 DOI、URL、页码、卷号、出版社、会议系列、article number 等重要元数据。
- 对无法可靠确认的信息标注 `需核实`，不编造缺失信息。

### 如何使用

将该 skill 安装或复制到你的 Codex skills 目录中，然后显式调用它，或直接让 Codex 规范化 BibTeX 引用。

示例 prompt：

```text
Use $bibtex-reference-normalizer to standardize the following BibTeX references for an IEEE paper.

[在这里粘贴 BibTeX 条目]
```

期望输出：

1. 修改后的完整 BibTeX 条目。
2. 每条引用的简短修改说明。
3. 对无法可靠核实的字段标注 `需核实`。

### 文件结构

```text
SKILL.md
agents/openai.yaml
```

`SKILL.md` 包含引用规范化规则。`agents/openai.yaml` 提供 Codex UI 元数据。
