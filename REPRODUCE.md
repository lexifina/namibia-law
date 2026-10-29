# How this repository was made (Namibia)

This file is written by the build on 2026-10-29, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
| NamibLII (Namibia Legal Information Institute: Law Reform and Development Commission, Ministry of Justice, on the Laws.Africa Peachjam platform) | <https://namiblii.org> | 2026-10-28 | CC BY-NC 4.0, crediting NamibLII as the source (https://namiblii.org/en/terms-of-use/, section 9) |
| Internet Archive Wayback Machine | <https://web.archive.org> | 2026-10-28 | Archived copies of NamibLII pages; the content licence is NamibLII's |
| NamibLII (Namibia Legal Information Institute), point-in-time expressions of the Income Tax, Customs and Excise and Value-Added Tax Acts | <https://namiblii.org> | 2026-10-29 | CC BY-NC 4.0, crediting NamibLII as the source (https://namiblii.org/en/terms-of-use/, section 9) |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `constitution` | Namibian Constitution | 1 | 2014-10-13 to 2014-10-13 |
| `labour` | Labour Act, 2007 | 2 | 2012-08-01 to 2023-03-15 |
| `companies` | Companies Act, 2004 | 3 | 2017-01-16 to 2023-07-21 |
| `income-tax` | Income Tax Act, 1981 | 2 | 2023-03-15 to 2024-09-16 |
| `customs-excise` | Customs and Excise Act, 1998 | 2 | 2022-02-23 to 2022-05-04 |
| `vat` | Value-Added Tax Act, 2000 | 2 | 2023-03-15 to 2024-10-01 |

The build made 14 commits:

| Commits | Kind |
| ---: | --- |
| 6 | first version of an act |
| 7 | one law on its in-force day |
| 1 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-29.
- 0 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 98 laws in the record.
- 19 tags.

## Dates

Each commit is dated at noon (Africa/Windhoek) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Not applied: every version is dated by NamibLII's own expression date, the day the amendment it incorporates took effect as Laws.Africa records it. No date is computed from a default rule. https://namiblii.org/legislation/

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `540ab9f431b82228b15b79343552d271ffbfa8c7711e508f766de868309c501e` (2708428 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3d00541d258745461ab52b1b0cb4e1716a27a95d`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.12.10; git version 2.46.0.windows.1.

## Checks

12 versions of 6 acts read back from git on the day each took effect and on the day before: 0 mismatches. Trailers: 0 commits whose trailers git cannot parse. Health: 0 merge commits on main, 0 commit dates that go backwards, 0 commits dated after the build.

A second build from the same corpus into an empty folder gave identical hashes for all 14 history commits and 19 tags (history tip `c9cb2266c5128194bc84d5a8a7d77320bb8245f6`).

## Decisions made by hand

- Acts were chosen by what the archived source supports: every expression NamibLII lists for the Labour Act 2007 (2) and the Companies Act 2004 (3) has a complete Internet Archive copy, so each version is read from its own dated expression.
- The Namibian Constitution has one NamibLII expression, 2014-10-13, which takes in the First (Act 34 of 1998, 1998-12-24), Second (Act 7 of 2010, 2010-05-07) and Third (Act 8 of 2014, 2014-10-13) Amendment Acts; NamibLII publishes no earlier expression. The original text (Government Gazette 2 of 21 March 1990) and the three amending Acts exist only as scanned Gazette PDFs (the 1990 Gazette's only text layer is an unreliable OCR layer of the scan), and no OCR is used, so the Constitution's history before 2014-10-13 is not rebuilt: its one version is the oldest available, credited to NamibLII.
- The Criminal Procedure Act 51 of 1977 was tried and left out: NamibLII lists 4 expressions (2014-01-01, 2019-01-30, 2023-07-25, 2024-05-15), but every Internet Archive copy of the 2023-07-25 expression is cut off (at 1 MiB) or empty, so the Criminal Procedure Amendment Act 2023's changes could only be dated 2024-05-15, about ten months late.
- Licence: NamibLII licenses primary and secondary law content CC BY-NC 4.0, crediting NamibLII as the source; CC BY-NC allows only non-commercial use. Every version is read from the Internet Archive's copy, for the configured acts only. No legal text was given to a model.
- Amending laws carry no enacted or published dates: their NamibLII pages show only the Gazette PDF, which was not read.
- Version dates are NamibLII's expression dates. Laws.Africa's terminology guide (https://docs.laws.africa/getting-started/terminology-guide) says "Amendments to Principal works come into force on the Commencement date of the Amending work" and that the first point in time is "the work as originally published"; so an amendment's expression is dated by its commencement (in force), and an act's original expression by its publication, which is replaced by the commencement date the page states.
- Credits: a version whose History names exactly one amending law (and no consolidation) between it and the previous version is credited to that law for every provision that changed. Otherwise a provision is credited only to laws that NamibLII's editorial note inside that provision links to; the rest are unexplained (publisher).
- Editorial notes (akn-remark) are left out of the text and used only as credit evidence, except where a provision has no other text (repealed or spent), where the note is the provision's whole printed content.
- Part, Chapter and Division headings are left out; each provision file starts with its own number and heading. Every other text of each version is in a provision file: this is checked per version (verification.json, fidelity).
- Version dates are NamibLII's expression dates. Laws.Africa's terminology guide (https://docs.laws.africa/getting-started/terminology-guide) says "Amendments to Principal works come into force on the Commencement date of the Amending work" and that the first point in time is "the work as originally published"; so an amendment's expression is dated by its commencement (in force), and an act's original expression by its publication, which is replaced by the commencement date the page states.
- Credits: a version whose History names exactly one amending law (and no consolidation) between it and the previous version is credited to that law for every provision that changed. Otherwise a provision is credited only to laws that NamibLII's editorial note inside that provision links to; the rest are unexplained (publisher).
- Editorial notes (akn-remark) are left out of the text and used only as credit evidence, except where a provision has no other text (repealed or spent), where the note is the provision's whole printed content.
- Part, Chapter and Division headings are left out; each provision file starts with its own number and heading. Every other text of each version is in a provision file: Lexifina's code checks this per version (verification.json, fidelity).
- Income Tax Act: the LII lists expression(s) 2016-06-21, 2020-12-31, 2021-12-16, 2023-02-15, but the Internet Archive holds no copy, so their changes appear in the next version that is archived.
- Customs and Excise Act: the LII lists expression(s) 2017-03-31, 2017-11-15, 2018-02-21, 2019-08-02, 2019-10-16, 2020-02-26, 2020-06-12, 2021-01-01, 2022-01-01, but the Internet Archive holds no copy, so their changes appear in the next version that is archived.
- VAT Act: the LII lists expression(s) 2023-01-01, but the Internet Archive holds no copy, so their changes appear in the next version that is archived.
- Income Tax Act: the history starts at 2023-03-15 (oldest version kept): earlier archived versions (2023-01-01) are left out, because an expression NamibLII lists between them has no archived copy and its changes would otherwise be dated too late.
- Customs and Excise Act: the history starts at 2022-02-23 (oldest version kept): earlier archived versions (2018-08-01, 2019-05-28, 2020-03-12, 2020-04-27, 2021-04-16) are left out, because an expression NamibLII lists between them has no archived copy and its changes would otherwise be dated too late.
- VAT Act: the history starts at 2023-03-15 (oldest version kept): earlier archived versions (2016-01-01) are left out, because an expression NamibLII lists between them has no archived copy and its changes would otherwise be dated too late.

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote the configuration and chose the acts. No model wrote, summarised or transformed legal text: the text is parsed by Lexifina's shared deterministic code.
- Claude Code (Claude Opus 5.5, claude-opus-5-5) wrote the fetch script and configuration and chose the acts. No model wrote, summarised or transformed legal text: Lexifina's code is the shared adapter's deterministic code.
