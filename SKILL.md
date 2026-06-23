---
name: bibtex-reference-normalizer
description: Normalize BibTeX references for computer science and communications papers, especially IEEE-style journal/conference references, IEEE Access entries, ACM references, and arXiv preprints. Use when the user asks to modify, standardize, verify, or polish BibTeX references, citation formats, IEEE references, ACM references, conference locations, journal abbreviations, author truncation, title capitalization, or arXiv entries.
---

# BibTeX Reference Normalizer

Normalize BibTeX references according to the target publication style. Default to IEEE style unless the entry clearly belongs to ACM or the user specifies ACM Reference Format.

## Output Requirements

Always provide:

1. The corrected complete BibTeX entries.
2. A short change note for each entry.
3. `需核实` for any field that cannot be verified reliably.

Do not invent months, locations, pages, volume, issue number, article number, or DOI.

## General Rules

- Keep DOI, URL, article number, publisher, series, location, and address fields when they may be required by the target style.
- Delete empty fields such as `volume={}`, `number={}`, and `pages={}` unless the target template requires them.
- Ensure BibTeX keys are unique.
- Use BibTeX page ranges with double hyphens: `pages={18378--18391}`.
- Prefer verified metadata from DOI pages, IEEE Xplore, ACM Digital Library, publisher pages, journal websites, conference websites, or arXiv.

## Title Format

Use sentence case.

- Protect the first letter of the title with braces:
  `title={{H}igh-quality model aggregation for blockchain-based federated learning}`
- Protect the first letter after a colon:
  `title={{M}oTiCPS: {E}nergy optimization on multi-objective task scheduling in {IoT}-integrated cyber-physical systems}`
- Protect acronyms, proper nouns, standards, datasets, algorithms, protocols, and brand names:
  `{Internet of Things}`, `{IoT}`, `{Monte Carlo}`, `{IEEE}`, `{ACM}`, `{Wi-Fi}`, `{5G}`, `{COVID-19}`.
- Do not convert ordinary technical phrases to title case. Usually keep phrases such as `federated learning`, `multi-task learning`, and `cyber-physical systems` lowercase unless they are part of a proper noun.
- Do not capitalize every word.

## Author Format

For IEEE style:

- If there are more than 6 authors, keep the first author and replace the rest with `and others`.
- If there are 6 or fewer authors, keep all authors.
- Do not use "more than 5 authors" as the IEEE truncation rule.

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

## IEEE Conference Papers

Use IEEE-style abbreviated `booktitle` when appropriate:

```bibtex
booktitle={Proc. IEEE Int. Conf. Blockchain (Blockchain)}
```

Do not mechanically delete the conference year or edition number. Decide based on the official conference name, IEEE Xplore page, and target template.

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

Examples:

```bibtex
address={Los Angeles, CA, USA}
address={London, U.K.}
address={Dubai, U.A.E.}
address={Rhodes, Greece}
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

Prefer `@misc`, or `@preprint` if the target template supports it.

Do not write arXiv entries as:

```bibtex
journal={arXiv preprint:2403.00561}
```

Preferred format:

```bibtex
@MISC{Yuan2024MultiTaskLU,
  author={Yuan, Huaqing and He, Yi and Du, Peng and Song, Lu},
  title={{M}ulti-task learning using uncertainty to weigh losses for heterogeneous face attribute estimation},
  year={2024},
  month={Mar.},
  eprint={2403.00561},
  archivePrefix={arXiv},
  doi={10.48550/arXiv.2403.00561}
}
```

## Verification Checklist

For each entry, verify when possible:

1. Journal or conference name.
2. Official abbreviation.
3. Author list.
4. Year, month, volume, issue number, pages, or article number.
5. DOI.
6. Conference location.

If a field cannot be verified, preserve the original value when reasonable and mention `需核实` in the change note.
