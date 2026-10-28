# How this repository was made (Namibia)

This file is written by the build on 2026-10-28, the day the source data was retrieved. Everything below is enough to rebuild this repository hash for hash.

## Sources

| Source | Address | Retrieved | Requests | Licence |
| --- | --- | --- | ---: | --- |
| NamibLII (Namibia Legal Information Institute: Law Reform and Development Commission, Ministry of Justice, on the Laws.Africa Peachjam platform) | <https://namiblii.org> | 2026-10-28 | 114 | CC BY-NC 4.0, crediting NamibLII as the source (https://namiblii.org/en/terms-of-use/, section 9) |
| Internet Archive Wayback Machine | <https://web.archive.org> | 2026-10-28 | None | Archived copies of NamibLII pages; the content licence is NamibLII's |

Every response is cached by the sha256 of its URL, and the table above lists every source with its retrieval date. Lexifina keeps its fetch scripts privately; `tools/parse.py` reads only the cache and writes `corpus.json`, so the same cache always gives the same corpus.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | Namibian Constitution | 1 | 2014-10-13 to 2014-10-13 |
| `labour` | Labour Act, 2007 | 2 | 2012-08-01 to 2023-03-15 |
| `companies` | Companies Act, 2004 | 3 | 2017-01-16 to 2023-07-21 |

The build made 5 commits:

| Commits | Kind |
| ---: | --- |
| 3 | first version of an act |
| 2 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-28.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 8 laws in the record.
- 8 tags.

## Dates

Each commit is dated at noon (Africa/Windhoek) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Not applied: every version is dated by NamibLII's own expression date, the day the amendment it incorporates took effect as Laws.Africa records it. No date is computed from a default rule. https://namiblii.org/legislation/

## Commands, in order

```sh
# fill the cache from the sources listed above (network; Lexifina's fetch scripts are kept privately)
python -X utf8 tools/parse.py                  # cache -> corpus.json (no network)
python -X utf8 tools/build.py <folder> --repo <empty folder> --docs-date 2026-10-28
python -X utf8 tools/check_repo.py <repo> --corpus <folder>/corpus.json --write
python -X utf8 tools/build.py <folder> --repo <another empty folder> --docs-date 2026-10-28 --compare <repo>
```

In the main Lexifina repository these files live as follows:
- `fetch.py`, `parse.py` and `repo/`: in `scripts/namibia-law/`.
- `build.py`, `check_repo.py` (`check.py` there) and `on.py`: in `scripts/gitlaw_common/`, with the corpus format in `SCHEMA.md`.

## Exact inputs

- `corpus.json` sha256 `b591f03539bf27e7acd77ed237c3eb7b3e9a9d60d42976117b10f76653501542` (1430374 bytes)
- Script blob hashes (`git hash-object`):

| Script | Blob |
| --- | --- |
| build.py | `833a2433a3ea96fd87477ccc7a2ed47dc9e24b48` |
| check.py | `426d4cfb32ce103715be6a00865c0a7bca81a56a` |
| on.py | `644a6c0857fbcc72562032b58d57aa113fee0641` |
| fetch.py | `3c799cb31fba80866f936dcee4463680ea38f953` |
| parse.py | `5f403aa0373e9a9553ef7da5404da8ffce5a81f9` |

- Tools:
  - Python 3.14.0
  - git version 2.52.0.windows.1
  - curl 8.21.0 (Windows) libcurl/8.21.0 Schannel zlib/1.3.2 WinIDN WinLDAP

## Checks

Not yet run for this build.

Not yet run for this build.

These results are from the check run on the build before this one, from the same corpus.

## Decisions made by hand

- Acts were chosen by what the archived source supports: every expression NamibLII lists for the Labour Act 2007 (2) and the Companies Act 2004 (3) has a complete Internet Archive copy, so each version is read from its own dated expression.
- The Namibian Constitution has one NamibLII expression, 2014-10-13, which takes in the First (Act 34 of 1998, 1998-12-24), Second (Act 7 of 2010, 2010-05-07) and Third (Act 8 of 2014, 2014-10-13) Amendment Acts; NamibLII publishes no earlier expression. The original text (Government Gazette 2 of 21 March 1990) and the three amending Acts exist only as scanned Gazette PDFs (the 1990 Gazette's only text layer is an unreliable OCR layer of the scan), and no OCR is used, so the Constitution's history before 2014-10-13 is not rebuilt: its one version is the oldest available, credited to NamibLII.
- The Criminal Procedure Act 51 of 1977 was tried and left out: NamibLII lists 4 expressions (2014-01-01, 2019-01-30, 2023-07-25, 2024-05-15), but every Internet Archive copy of the 2023-07-25 expression is cut off (at 1 MiB) or empty, so the Criminal Procedure Amendment Act 2023's changes could only be dated 2024-05-15, about ten months late.
- Licence and terms: NamibLII licenses primary and secondary law content CC BY-NC 4.0, crediting NamibLII as the source; its terms say "Scraping and bulk downloading from this website is strictly prohibited"; its robots.txt sends Content-Signal search=yes, ai-train=no, use=reference and disallows CCBot, ClaudeBot and other AI crawlers. No NamibLII document page was fetched: every version is read from the Internet Archive's copy, through the shared machine-wide rate, for the configured acts only; NamibLII itself was asked only for robots.txt, its terms and one open listing page per act. The user decided on 2026-10-28 that reading these archived copies is acceptable (relayed by the coordinator: "scraping wayback is fair game, dont overdo it"). The repository stays private; CC BY-NC allows only non-commercial use. No legal text was given to a model.
- Amending laws carry no enacted or published dates: their NamibLII pages show only the Gazette PDF, so they were not fetched (scripts/africa-law/ISSUES-namibia.md, item 2).
- Version dates are NamibLII's expression dates. Laws.Africa's terminology guide (https://docs.laws.africa/getting-started/terminology-guide) says "Amendments to Principal works come into force on the Commencement date of the Amending work" and that the first point in time is "the work as originally published"; so an amendment's expression is dated by its commencement (in force), and an act's original expression by its publication, which is replaced by the commencement date the page states.
- Credits: a version whose History names exactly one amending law (and no consolidation) between it and the previous version is credited to that law for every provision that changed. Otherwise a provision is credited only to laws that NamibLII's editorial note inside that provision links to; the rest are unexplained (publisher).
- Editorial notes (akn-remark) are left out of the text and used only as credit evidence, except where a provision has no other text (repealed or spent), where the note is the provision's whole printed content.
- Part, Chapter and Division headings are left out; each provision file starts with its own number and heading. Every other text of each version is in a provision file: parse.py checks this per version (verification.json, fidelity).

## What AI did and did not do

The fetch, parse and check scripts were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above, through code that anyone can rerun.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote the fetch script and configuration and chose the acts. No model wrote, summarised or transformed legal text: parse.py is the shared adapter's deterministic code.
