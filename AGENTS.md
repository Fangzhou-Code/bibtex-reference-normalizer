# Agent Instructions: BibTeX Reference Normalizer

## English

Use these instructions when an AI agent is asked to normalize, verify, or polish BibTeX references for computer science and communications papers.

Default to IEEE style unless the user specifies another target venue or the entry clearly belongs to ACM.

### Required Output

1. Return the corrected complete BibTeX entries.
2. Add a short change note for each entry.
3. Mark uncertain metadata as `needs verification` in English output or `需核实` in Chinese output.
4. Do not invent months, conference locations, page ranges, volume numbers, issue numbers, article numbers, or DOIs.

### Core Rules

- Keep DOI, URL, article number, publisher, series, location, and address fields when the target style may require them.
- Remove empty fields such as `volume={}`, `number={}`, and `pages={}` unless the target template requires them.
- Ensure BibTeX keys are unique.
- Use double hyphens for page ranges, for example `pages={18378--18391}`.
- Verify metadata with reliable sources when possible: DOI pages, IEEE Xplore, ACM Digital Library, publisher pages, journal websites, conference websites, or arXiv.

### Title Format

Use sentence case. Protect required capitalization with BibTeX braces:

- Title first letter: `title={{H}igh-quality model aggregation for blockchain-based federated learning}`
- First letter after a colon: `title={{M}oTiCPS: {E}nergy optimization on multi-objective task scheduling in {IoT}-integrated cyber-physical systems}`
- Acronyms and proper nouns: `{IoT}`, `{IEEE}`, `{ACM}`, `{Wi-Fi}`, `{5G}`, `{Monte Carlo}`, `{Internet of Things}`

Do not convert ordinary technical phrases to title case unless they are proper nouns, standards, system names, datasets, or acronyms.

### Authors

For IEEE style, if there are more than 6 authors, keep the first author and replace the rest with `and others`. If there are 6 or fewer authors, keep all authors.

For ACM style, usually keep the full author list unless the venue requires abbreviation.

### IEEE Access

For IEEE Access entries:

- Use `journal={IEEE Access}` exactly.
- Usually do not add `month`.
- Usually do not add `number`.
- Keep `year`, `volume`, `pages`, and `doi`.

### IEEE Conference Locations

If verified, use `address` in this order:

- United States: `address={City, ST, USA}`
- United Kingdom: `address={City, U.K.}`
- United Arab Emirates: `address={City, U.A.E.}`
- Other countries: `address={City, Country}`

Do not invent locations for online, hybrid, or unverified conferences.

### ACM

Do not force ACM entries into IEEE style. ACM entries often retain full author lists and may use `booktitle={Proceedings of ...}`, `series`, `location`, `publisher={Association for Computing Machinery}`, and `address={New York, NY, USA}`.

### arXiv

Prefer `@misc` or a target-template-supported `@preprint`. Use `eprint`, `archivePrefix={arXiv}`, and DOI when available. Do not use `journal={arXiv preprint:...}` unless the target venue specifically asks for it.

## 中文

当 AI agent 需要规范化、核查或润色计算机与通信领域论文的 BibTeX 引用时，使用这些规则。

默认按 IEEE 风格处理，除非用户指定其他目标期刊/会议，或条目明显属于 ACM。

### 输出要求

1. 输出修改后的完整 BibTeX 条目。
2. 为每条引用添加简短修改说明。
3. 英文输出中将无法确认的信息标注为 `needs verification`，中文输出中标注为 `需核实`。
4. 不要编造月份、会议地点、页码、卷号、期号、article number 或 DOI。

### 核心规则

- 保留 DOI、URL、article number、publisher、series、location、address 等目标格式可能需要的字段。
- 删除空字段，例如 `volume={}`、`number={}`、`pages={}`，除非目标模板要求保留。
- 确保 BibTeX key 唯一。
- 页码范围使用双连字符，例如 `pages={18378--18391}`。
- 尽量通过 DOI 页面、IEEE Xplore、ACM Digital Library、出版社页面、期刊官网、会议官网或 arXiv 核查元数据。

### 标题格式

标题采用 sentence case，并用 BibTeX 大括号保护必要的大写：

- 标题首字母：`title={{H}igh-quality model aggregation for blockchain-based federated learning}`
- 冒号后首字母：`title={{M}oTiCPS: {E}nergy optimization on multi-objective task scheduling in {IoT}-integrated cyber-physical systems}`
- 缩写和专有名词：`{IoT}`、`{IEEE}`、`{ACM}`、`{Wi-Fi}`、`{5G}`、`{Monte Carlo}`、`{Internet of Things}`

不要把普通技术短语改成标题式大写，除非它是专有名词、标准、系统名、数据集名或缩写。

### 作者

IEEE 风格下，作者超过 6 人时保留第一作者并用 `and others` 表示其余作者；6 人及以下保留全部作者。

ACM 风格下通常保留完整作者列表，除非目标会议或模板明确要求缩写。

### IEEE Access

IEEE Access 条目：

- 使用 `journal={IEEE Access}`，不要缩写。
- 通常不添加 `month`。
- 通常不添加 `number`。
- 保留 `year`、`volume`、`pages` 和 `doi`。

### IEEE 会议地点

如能核实地点，按以下顺序使用 `address`：

- 美国：`address={City, ST, USA}`
- 英国：`address={City, U.K.}`
- 阿联酋：`address={City, U.A.E.}`
- 其他国家：`address={City, Country}`

对于线上、混合或无法核实地点的会议，不要编造地点。

### ACM

不要把 ACM 条目强行改成 IEEE 风格。ACM 条目通常保留完整作者，并可能使用 `booktitle={Proceedings of ...}`、`series`、`location`、`publisher={Association for Computing Machinery}`、`address={New York, NY, USA}` 等字段。

### arXiv

优先使用 `@misc`，或目标模板支持的 `@preprint`。尽量使用 `eprint`、`archivePrefix={arXiv}` 和 DOI。不建议使用 `journal={arXiv preprint:...}`，除非目标出版物明确要求。
