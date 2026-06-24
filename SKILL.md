---
name: bibtex-reference-normalizer
description: Normalize, verify, and complete BibTeX references for computer science and communications papers, especially IEEE-style journal/conference references, IEEE Access entries, ACM references, and arXiv preprints. Use when the user asks to modify, standardize, verify, polish, or complete BibTeX references from partial metadata such as title, DOI, arXiv ID, author names, venue names, or incomplete citation text.
---

# BibTeX Reference Normalizer

Normalize BibTeX references according to the target publication style. Default to IEEE style unless the entry clearly belongs to ACM or the user specifies ACM Reference Format. When the user provides only partial metadata, search reliable sources when network access is available, reconstruct the BibTeX entry from verified metadata, then normalize it.

## Style Precedence

Apply rules in this order:

1. The user's explicit target venue, template, or project-specific guide, if provided.
2. Official publisher metadata and style guides.
3. This skill's default rules.

If the user does not provide a target style or venue, infer them from the reference itself. Use DOI, arXiv ID, publisher pages, IEEE Xplore, ACM Digital Library, DBLP, Crossref, official venue pages, and the entry's `journal` or `booktitle` fields. Do not ask the user for target style or venue unless the reference is ambiguous after lookup.

Apply author truncation after more than 5 authors unless the target venue explicitly requires a different rule. Apply project-specific choices when requested, such as `UK` for United Kingdom conference locations or `United Arab Emirates` for UAE conference locations.

## Output Requirements

Always provide:

1. The corrected complete BibTeX entries.
2. A short change note for each entry.
3. `需核实` for any field that cannot be verified reliably.
4. Source hints used for completion when metadata was searched or inferred, such as DOI, IEEE Xplore, ACM Digital Library, arXiv, DBLP, Crossref, Semantic Scholar, publisher page, or official conference page.

Do not invent months, locations, pages, volume, issue number, article number, or DOI.

## Metadata Completion Workflow

Use this workflow when the user provides only a title, DOI, arXiv ID, partial author list, venue name, screenshot text, or incomplete citation.

1. Identify the strongest lookup key:
   - DOI: resolve the DOI first.
   - arXiv ID: query arXiv or the arXiv landing page first.
   - Exact title: search the exact title in quotation marks first.
   - Partial title plus authors/year/venue: search using the most specific combination.
2. Infer the publication type, target style, and venue from the lookup result:
   - IEEE journal/conference metadata -> IEEE style.
   - IEEE Access metadata -> IEEE Access rules.
   - ACM Digital Library metadata -> ACM style.
   - arXiv-only metadata -> arXiv/preprint rules.
   - Book metadata -> textbook rules.
3. Prefer authoritative sources in this order:
   - For IEEE journal or conference papers, IEEE Xplore original BibTeX export when available.
   - DOI registration page or Crossref metadata.
   - Publisher or digital library page, especially ACM Digital Library, SpringerLink, Elsevier ScienceDirect, Wiley, USENIX, ACL Anthology, or arXiv.
   - DBLP for computer science venue, author, year, and DOI cross-checking.
   - Google Scholar BibTeX for papers not available from IEEE Xplore or the publisher.
   - Google Books or Google Scholar for textbooks.
   - Semantic Scholar, OpenAlex, Google Scholar snippets, or general web search only as secondary evidence.
4. If an official BibTeX export exists, use it as the base entry, then apply this skill's normalization rules.
5. If no BibTeX export exists, construct the entry from verified metadata only.
6. Treat a match as reliable only when the title matches exactly or near-exactly and at least one additional field agrees, such as author, year, venue, DOI, or arXiv ID.
7. If multiple plausible records exist, do not guess. Ask the user to choose or mark ambiguous fields as `需核实`.
8. If the agent has no internet access or cannot verify a field, preserve the provided value when reasonable and mark missing or uncertain fields as `需核实`.

For title-only input, the expected behavior is: search the exact title, identify the correct publication record, collect authors, title, venue, year, volume/number/pages or article number, month when required and reliable, DOI or arXiv ID, then output a complete normalized BibTeX entry.

## General Rules

- Keep DOI, URL, article number, publisher, series, location, and address fields when they may be required by the target style.
- Delete empty fields such as `volume={}`, `number={}`, and `pages={}` unless the target template requires them.
- Ensure BibTeX keys are unique.
- Use BibTeX page ranges with double hyphens: `pages={18378--18391}`.
- Prefer verified metadata from DOI pages, IEEE Xplore, ACM Digital Library, publisher pages, journal websites, conference websites, DBLP, Crossref, Semantic Scholar, OpenAlex, or arXiv.
- For IEEE submissions, prefer BibTeX exported from IEEE Xplore for IEEE journal and conference papers. For non-IEEE papers, use publisher metadata first and Google Scholar BibTeX only when stronger sources are unavailable. For textbooks, Google Books or publisher pages may be useful sources.

## Title Format

Use sentence case.

- Protect the first letter of the title with braces:
  `title={{H}igh-quality model aggregation for blockchain-based federated learning}`
- Protect the first letter after a colon:
  `title={{M}oTiCPS: {E}nergy optimization on multi-objective task scheduling in {IoT}-integrated cyber-physical systems}`
- Protect acronyms, proper nouns, standards, datasets, algorithms, protocols, and brand names:
  `{Internet of Things}`, `{IoT}`, `{Monte Carlo}`, `{IEEE}`, `{ACM}`, `{Wi-Fi}`, `{5G}`, `{COVID-19}`.
- Also protect communication and mathematics terms that must retain capitalization, such as `{2G}`, `{3G}`, `{4G}`, `{5G}`, `{6G}`, `{WLAN}`, `{Bluetooth}`, `{LTE}`, `{Internet}`, `{MIMO}`, `{MISO}`, `{SIMO}`, `{OFDM}`, `{OFDMA}`, `{NOMA}`, `{RSMA}`, `{mmWave}`, `{RF}`, `{CSI}`, `{RSSI}`, `{RIS}`, `{IRS}`, `{Gauss}`, `{Gaussian}`, `{Markov}`, `{Markovian}`, `{Rayleigh}`, `{Rice}`, `{Rician}`, `{Nakagami}`, `{FedAvg}`, and `{Hybrid-FL}`.
- Do not convert ordinary technical phrases to title case. Usually keep phrases such as `federated learning`, `multi-task learning`, and `cyber-physical systems` lowercase unless they are part of a proper noun.
- Do not capitalize every word.

## Author Format

For IEEE style:

- If there are more than 5 authors, keep the first author and replace the rest with `and others`.
- If there are 5 or fewer authors, keep all authors.

Example:

```bibtex
author={Qi, Jiahao and others}
```

For ACM style:

- Usually keep the full author list unless the target template or venue explicitly requires abbreviation.

## IEEE Journal Articles

For IEEE journal entries, generally keep:

```text
author, journal, title, year, volume, number, pages, doi
```

Use official journal abbreviations. Prefer IEEE official abbreviations, ACM official format, ISO 4/LTWA, publisher pages, or journal websites. Do not rely only on ordinary web search results.

If the month is reliable, add:

```bibtex
month={Oct.}
```

Use month abbreviations:

```text
Jan., Feb., Mar., Apr., May, June, July, Aug., Sept., Oct., Nov., Dec.
```

Some target styles also permit `Jun.` for June, `Jul.` for July, and `Sep.` for September. Keep one style consistent within the same bibliography.

### IEEE Access

For `IEEE Access` entries:

- Use `journal={IEEE Access}` exactly.
- Do not abbreviate `IEEE Access`.
- Usually do not add `month`.
- Usually do not add `number`.
- Keep `year`, `volume`, `pages`, and `doi`.
- If an original entry has `month` or an empty `number`, usually remove it.
- Do not say IEEE Access does not need a date. It usually does not need a month, but it does need a year.

Example:

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

### IEEE Early Access Journal Articles

For IEEE early-access journal articles that do not yet have final volume, issue, page, month, or year metadata:

- Prefer the original IEEE Xplore BibTeX export.
- Leave `year`, `volume`, `number`, and `pages` blank if the target template expects those fields to exist; otherwise remove empty fields only if the target style allows it.
- Do not invent final volume, issue, page, month, or year values.
- Add the early access date and DOI in `note`, using the Date of Publication from IEEE Xplore.
- Keep the `doi` field as well when present.

Example:

```bibtex
@ARTICLE{11409469,
  author={Li, Taoshen and Dang, Shuping and Ge, Zhihui and Xu, Yihang and Zhang, Zhenrong},
  journal={IEEE Trans. Veh. Technol.},
  title={{C}ramer-von {M}ises criterion based parametric mapping for channel model substitution},
  year={},
  volume={},
  number={},
  pages={},
  note={early access, Feb. 24, 2026, doi: 10.1109/TVT.2026.3667726},
  doi={10.1109/TVT.2026.3667726}
}
```

## IEEE Conference Papers

Use IEEE-style abbreviated `booktitle` when appropriate:

```bibtex
booktitle={Proc. IEEE Int. Conf. Blockchain (Blockchain)}
```

Remove the conference year and ordinal edition number from `booktitle` by default. Keep the publisher/society name, abbreviated conference name, and official acronym in parentheses. Still verify the conference name from IEEE Xplore, ACM Digital Library, the official conference page, or reputable published references.

```bibtex
booktitle={Proc. IEEE Int. Conf. Commun. Control Comput. Technol. Smart Grids (SmartGridComm)}
```

If the conference month is reliable, add:

```bibtex
month={Nov.}
```

If the conference location is reliable, add `address`.

Apply location format in this order:

- United States: `address={City, ST, USA}`
- United Kingdom: `address={City, U.K.}`
- United Arab Emirates: `address={City, U.A.E.}`
- Other countries: `address={City, Country}`

If the target style requests it, use `UK` rather than `U.K.` and `United Arab Emirates` rather than `U.A.E.` or `UAE`.

Examples:

```bibtex
address={Los Angeles, CA, USA}
address={London, U.K.}
address={Dubai, U.A.E.}
address={Rhodes, Greece}
address={London, UK}
address={Dubai, United Arab Emirates}
```

Keep `pages` and `doi`.

If the conference was online, hybrid, or the location cannot be verified, do not invent a location. Keep the original field or mark it as `需核实`.

Example:

```bibtex
@INPROCEEDINGS{9284689,
  author={Passerat-Palmbach and others},
  booktitle={Proc. IEEE Int. Conf. Blockchain (Blockchain)},
  title={{B}lockchain-orchestrated machine learning for privacy preserving federated learning in electronic health data},
  year={2020},
  month={Nov.},
  address={Rhodes, Greece},
  pages={550--555},
  doi={10.1109/Blockchain50366.2020.00080}
}
```

## ACM Entries

If the target is ACM, do not force IEEE style.

ACM entries usually keep complete author lists and may use fields such as:

```bibtex
booktitle={Proceedings of ...},
series={...},
location={...},
publisher={Association for Computing Machinery},
address={New York, NY, USA}
```

Do not mechanically convert ACM `location`, `publisher`, and `address` fields into IEEE-style `address`.

Use ACM Digital Library metadata, ACM templates, or the venue-provided `.bst` / `.cls` files when available.

## arXiv and Preprints

Before citing a preprint, check whether a formally published or peer-reviewed version exists. If it exists and is the version the paper should cite, cite the published version instead of the preprint.

Use `@ARTICLE` for arXiv entries in this project.

arXiv references must include the arXiv identifier. Use the base official form `arXiv:YYMM.NNNNN` for newer identifiers, such as `arXiv:2403.00561`, without version number or subject class unless the target venue explicitly asks for them. For older identifiers, preserve the archive prefix form, such as `arXiv:hep-th/9901001`. Keep the identifier contiguous; do not insert spaces or extra punctuation inside it.

Write the arXiv identifier in the `journal` field:

```bibtex
journal={arXiv preprint:2403.00561}
```

Preferred format:

```bibtex
@ARTICLE{Yuan2024MultiTaskLU,
  author={Yuan, Huaqing and He, Yi and Du, Peng and Song, Lu},
  journal={arXiv preprint:2403.00561},
  title={{M}ulti-task learning using uncertainty to weigh losses for heterogeneous face attribute estimation},
  year={2024},
  month={Mar.}
}
```

For arXiv entries, verify the base arXiv identifier and submission/revision date from the arXiv page. Do not include version number or subject class by default. Do not include `note`, `url`, or `doi` for arXiv entries unless the target venue explicitly requires them.

## Textbooks

For textbooks:

- Prefer publisher pages, Google Books, or Google Scholar BibTeX when official metadata is unavailable.
- Keep book metadata complete: author/editor, title, edition, publisher, address/location when available, year, ISBN or DOI if relevant.
- When citing a specific chapter, equation, theorem, or page in LaTeX, put the locator in the citation command rather than modifying the BibTeX entry.

Examples:

```tex
\cite[Ch. 2]{cover2012elements}
\cite[Eq. (9.17)]{cover2012elements}
```

## Verification Checklist

For each entry, verify when possible:

1. Journal or conference name.
2. Official abbreviation.
3. Author list.
4. Year, month, volume, issue number, pages, or article number.
5. DOI or arXiv ID.
6. Conference location.
7. Whether the selected record is unambiguous when the input was partial.
8. Whether a preprint has a formally published version.
9. Whether an IEEE article is early access and lacks final volume/issue/page metadata.

If a field cannot be verified, preserve the original value when reasonable and mention `需核实` in the change note.
