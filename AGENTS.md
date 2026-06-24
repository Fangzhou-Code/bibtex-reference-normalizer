# Agent Instructions: BibTeX Reference Normalizer

## English

Use these instructions when an AI agent is asked to normalize, verify, polish, or complete BibTeX references for computer science and communications papers. Default to IEEE style unless the user specifies another target venue or the entry clearly belongs to ACM.

### Style Precedence

Apply the user's target venue, template, or project-specific guide first. Unless the target venue explicitly requires a different rule, truncate authors when there are more than 5 authors. Apply project-specific choices when requested, such as `UK` for United Kingdom conference locations, `United Arab Emirates` for UAE conference locations, and IEEE early-access entries with a `note` field containing early access date and DOI.

### Required Output

1. Return the corrected complete BibTeX entries.
2. Add a short change note for each entry.
3. Mark uncertain metadata as `needs verification` in English output or `需核实` in Chinese output.
4. Include source hints when metadata was searched or inferred.
5. Do not invent months, conference locations, page ranges, volume numbers, issue numbers, article numbers, or DOIs.

### Partial Metadata Completion

When the user provides only a paper title, DOI, arXiv ID, partial author list, venue name, screenshot text, or incomplete citation, search and complete the record if network access is available.

1. Use the strongest lookup key first: DOI, arXiv ID, exact title, then partial title plus author/year/venue.
2. Prefer authoritative sources: IEEE Xplore original BibTeX for IEEE papers; DOI/Crossref; publisher pages; ACM Digital Library, SpringerLink, Elsevier ScienceDirect, Wiley, USENIX, ACL Anthology, arXiv, DBLP; Google Scholar BibTeX for papers unavailable from stronger sources; Google Books or publisher pages for textbooks; then secondary sources such as Semantic Scholar, OpenAlex, Google Scholar snippets, or general web search.
3. If an official BibTeX export exists, use it as the base entry and then normalize it.
4. If no BibTeX export exists, construct the entry only from verified metadata.
5. Treat a match as reliable only when the title matches exactly or near-exactly and at least one additional field agrees, such as author, year, venue, DOI, or arXiv ID.
6. If multiple plausible records exist, ask the user to choose or mark ambiguous fields as `needs verification` / `需核实`.
7. If the agent lacks internet access or cannot verify a field, preserve provided information when reasonable and mark missing or uncertain fields.

### Core Rules

- Keep DOI, URL, article number, publisher, series, location, and address fields when the target style may require them.
- Remove empty fields such as `volume={}`, `number={}`, and `pages={}` unless the target template requires them.
- Ensure BibTeX keys are unique.
- Use double hyphens for page ranges, for example `pages={18378--18391}`.
- Verify metadata with reliable sources when possible.
- For IEEE papers, prefer IEEE Xplore BibTeX when available. For textbooks, use publisher pages, Google Books, or Google Scholar when official metadata is unavailable.

### Title Format

Use sentence case. Protect required capitalization with BibTeX braces:

- Title first letter: `title={{H}igh-quality model aggregation for blockchain-based federated learning}`
- First letter after a colon: `title={{M}oTiCPS: {E}nergy optimization on multi-objective task scheduling in {IoT}-integrated cyber-physical systems}`
- Acronyms and proper nouns: `{IoT}`, `{IEEE}`, `{ACM}`, `{Wi-Fi}`, `{5G}`, `{Monte Carlo}`, `{Internet of Things}`
- Also protect common communications and mathematics terms when needed: `{2G}`, `{3G}`, `{4G}`, `{5G}`, `{6G}`, `{WLAN}`, `{Bluetooth}`, `{LTE}`, `{Internet}`, `{MIMO}`, `{MISO}`, `{SIMO}`, `{OFDM}`, `{OFDMA}`, `{NOMA}`, `{RSMA}`, `{mmWave}`, `{RF}`, `{CSI}`, `{RSSI}`, `{RIS}`, `{IRS}`, `{Gauss}`, `{Gaussian}`, `{Markov}`, `{Rayleigh}`, `{Rician}`, `{Nakagami}`, `{FedAvg}`, `{Hybrid-FL}`.

Do not convert ordinary technical phrases to title case unless they are proper nouns, standards, system names, datasets, or acronyms.

### Authors

If there are more than 5 authors, keep the first author and replace the rest with `and others`. If there are 5 or fewer authors, keep all authors.

For ACM style, usually keep the full author list unless the venue requires abbreviation.

### IEEE Access

For IEEE Access entries:

- Use `journal={IEEE Access}` exactly.
- Usually do not add `month`.
- Usually do not add `number`.
- Keep `year`, `volume`, `pages`, and `doi`.

### IEEE Early Access

For IEEE early-access journal articles without final volume, issue, page, month, or year metadata, do not invent final publication metadata. Prefer IEEE Xplore BibTeX, leave final fields blank if the template expects them, and add the early access date and DOI in `note`, for example:

```bibtex
note={early access, Feb. 24, 2026, doi: 10.1109/TVT.2026.3667726}
```

### IEEE Conference Locations

If verified, use `address` in this order:

- United States: `address={City, ST, USA}`
- United Kingdom: `address={City, U.K.}`
- United Arab Emirates: `address={City, U.A.E.}`
- Other countries: `address={City, Country}`

If the target style requests it, use `UK` and `United Arab Emirates` instead of `U.K.` and `U.A.E.`. Conference proceedings may retain the year after `Proc.` when that is the established form, such as `Proc. 2024 IEEE Int. Conf. ...`.

Do not invent locations for online, hybrid, or unverified conferences.

### ACM

Do not force ACM entries into IEEE style. ACM entries often retain full author lists and may use `booktitle={Proceedings of ...}`, `series`, `location`, `publisher={Association for Computing Machinery}`, and `address={New York, NY, USA}`.

### arXiv

Before citing a preprint, check whether a formally published or peer-reviewed version exists. Prefer `@misc` or a target-template-supported `@preprint`. Use `eprint`, `archivePrefix={arXiv}`, and DOI when available. Do not use `journal={arXiv preprint:...}` unless the target venue specifically asks for it. If a venue or guide asks for access month/year, include it in a target-supported field such as `note`.

### Textbooks

For textbooks, use publisher pages, Google Books, or Google Scholar metadata. Keep author/editor, title, edition, publisher, location, year, and ISBN/DOI when available. For a specific chapter, equation, theorem, or page, use LaTeX citation locators such as `\cite[Ch. 2]{key}` or `\cite[Eq. (9.17)]{key}` instead of changing the BibTeX entry.

## 中文

当 AI agent 需要规范化、核查、润色或补全计算机与通信领域论文的 BibTeX 引用时，使用这些规则。默认按 IEEE 风格处理，除非用户指定其他目标期刊/会议，或条目明显属于 ACM。

### 风格优先级

优先遵循用户指定的目标期刊/会议、模板或项目特定指南。除非目标 venue 明确要求其他规则，否则作者超过 5 人即缩写。按需应用项目特定规则，例如英国会议地点写 `UK`；阿联酋会议地点写 `United Arab Emirates`；IEEE early-access 条目用 `note` 字段写 early access 日期和 DOI。

### 输出要求

1. 输出修改后的完整 BibTeX 条目。
2. 为每条引用添加简短修改说明。
3. 英文输出中将无法确认的信息标注为 `needs verification`，中文输出中标注为 `需核实`。
4. 当元数据经过搜索或推断时，说明使用的来源线索。
5. 不要编造月份、会议地点、页码、卷号、期号、article number 或 DOI。

### 部分信息补全

当用户只提供论文标题、DOI、arXiv ID、部分作者、会议/期刊名、截图文字或不完整引用时，如果具备联网能力，应搜索并补全文献信息。

1. 优先使用最强检索键：DOI、arXiv ID、精确标题、再到标题片段加作者/年份/venue。
2. 优先使用权威来源：IEEE 论文优先使用 IEEE Xplore 原始 BibTeX；DOI/Crossref；出版社页面；ACM Digital Library、SpringerLink、Elsevier ScienceDirect、Wiley、USENIX、ACL Anthology、arXiv、DBLP；如果更强来源不可用，再使用 Google Scholar BibTeX；教材可使用 Google Books 或出版社页面；最后才使用 Semantic Scholar、OpenAlex、Google Scholar 摘要或普通网页作为辅助证据。
3. 如果官方页面提供 BibTeX 导出，以官方 BibTeX 为基础，再按本规则规范化。
4. 如果没有 BibTeX 导出，只用已核实的元数据构造条目。
5. 只有当标题精确或近似匹配，并且作者、年份、venue、DOI 或 arXiv ID 中至少一项也匹配时，才认为记录可靠。
6. 如果存在多个可能记录，不要猜测；请用户选择，或把有歧义字段标注为 `需核实`。
7. 如果 agent 无法联网或无法核实某字段，合理保留用户提供的信息，并标注缺失或不确定字段。

### 核心规则

- 保留 DOI、URL、article number、publisher、series、location、address 等目标格式可能需要的字段。
- 删除空字段，例如 `volume={}`、`number={}`、`pages={}`，除非目标模板要求保留。
- 确保 BibTeX key 唯一。
- 页码范围使用双连字符，例如 `pages={18378--18391}`。
- 尽量通过可靠来源核查元数据。
- IEEE 论文优先使用 IEEE Xplore 导出的 BibTeX。教材可使用出版社页面、Google Books 或 Google Scholar 元数据。

### 标题格式

标题采用 sentence case，并用 BibTeX 大括号保护必要的大写：

- 标题首字母：`title={{H}igh-quality model aggregation for blockchain-based federated learning}`
- 冒号后首字母：`title={{M}oTiCPS: {E}nergy optimization on multi-objective task scheduling in {IoT}-integrated cyber-physical systems}`
- 缩写和专有名词：`{IoT}`、`{IEEE}`、`{ACM}`、`{Wi-Fi}`、`{5G}`、`{Monte Carlo}`、`{Internet of Things}`
- 必要时也保护通信和数学领域常见大小写：`{2G}`、`{3G}`、`{4G}`、`{5G}`、`{6G}`、`{WLAN}`、`{Bluetooth}`、`{LTE}`、`{Internet}`、`{MIMO}`、`{MISO}`、`{SIMO}`、`{OFDM}`、`{OFDMA}`、`{NOMA}`、`{RSMA}`、`{mmWave}`、`{RF}`、`{CSI}`、`{RSSI}`、`{RIS}`、`{IRS}`、`{Gauss}`、`{Gaussian}`、`{Markov}`、`{Rayleigh}`、`{Rician}`、`{Nakagami}`、`{FedAvg}`、`{Hybrid-FL}`。

不要把普通技术短语改成标题式大写，除非它是专有名词、标准、系统名、数据集名或缩写。

### 作者

作者超过 5 人时保留第一作者并用 `and others` 表示其余作者；5 人及以下保留全部作者。

ACM 风格下通常保留完整作者列表，除非目标会议或模板明确要求缩写。

### IEEE Access

IEEE Access 条目：

- 使用 `journal={IEEE Access}`，不要缩写。
- 通常不添加 `month`。
- 通常不添加 `number`。
- 保留 `year`、`volume`、`pages` 和 `doi`。

### IEEE Early Access

对于尚无最终卷号、期号、页码、月份或年份的 IEEE early-access 期刊论文，不要编造最终出版信息。优先使用 IEEE Xplore BibTeX；如果模板需要这些字段，可将 `year`、`volume`、`number`、`pages` 留空；用 `note` 写 early access 日期和 DOI，例如：

```bibtex
note={early access, Feb. 24, 2026, doi: 10.1109/TVT.2026.3667726}
```

### IEEE 会议地点

如能核实地点，按以下顺序使用 `address`：

- 美国：`address={City, ST, USA}`
- 英国：`address={City, U.K.}`
- 阿联酋：`address={City, U.A.E.}`
- 其他国家：`address={City, Country}`

如果目标格式要求，英国写 `UK`，阿联酋写 `United Arab Emirates`。会议 proceedings 如有既定格式，可以在 `Proc.` 后保留年份，例如 `Proc. 2024 IEEE Int. Conf. ...`。

对于线上、混合或无法核实地点的会议，不要编造地点。

### ACM

不要把 ACM 条目强行改成 IEEE 风格。ACM 条目通常保留完整作者，并可能使用 `booktitle={Proceedings of ...}`、`series`、`location`、`publisher={Association for Computing Machinery}`、`address={New York, NY, USA}` 等字段。

### arXiv

引用预印本前，先检查是否已有正式发表或同行评议版本。优先使用 `@misc`，或目标模板支持的 `@preprint`。尽量使用 `eprint`、`archivePrefix={arXiv}` 和 DOI。不建议使用 `journal={arXiv preprint:...}`，除非目标出版物明确要求。如果 venue 或指南要求访问月份/年份，可放入 `note` 等目标模板支持的字段。

### 教材

教材优先使用出版社页面、Google Books 或 Google Scholar 元数据。尽量保留作者/编辑、书名、版次、出版社、地点、年份、ISBN/DOI。若引用具体章节、公式、定理或页码，应在 LaTeX 引用命令中指定，例如 `\cite[Ch. 2]{key}` 或 `\cite[Eq. (9.17)]{key}`，不要为此修改 BibTeX 条目。
